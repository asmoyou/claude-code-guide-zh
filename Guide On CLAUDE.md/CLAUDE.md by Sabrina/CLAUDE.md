# Claude 代码指南

## 实现最佳实践

### 0 — 目的  

这些规则确保可维护性、安全性和开发速度。
**MUST** 规则由CI强制执行；**SHOULD** 规则强烈推荐。

---

### 1 — 编码前

- **BP-1 (MUST)** 向用户提出澄清问题
- **BP-2 (SHOULD)** 为复杂工作起草并确认方法  
- **BP-3 (SHOULD)** 如果存在≥2种方法，列出明确的优缺点

---

### 2 — 编码时

- **C-1 (MUST)** 遵循TDD：搭建存根 -> 编写失败测试 -> 实现
- **C-2 (MUST)** 使用现有领域词汇命名函数以保持一致性  
- **C-3 (SHOULD NOT)** 当小型可测试函数足够时引入类  
- **C-4 (SHOULD)** 优先使用简单、可组合、可测试的函数
- **C-5 (MUST)** 优先使用带品牌的`type`作为ID
  ```ts
  type UserId = Brand<string, 'UserId'>   // ✅ 好
  type UserId = string                    // ❌ 不好
  ```  
- **C-6 (MUST)** 对仅类型导入使用`import type { … }`
- **C-7 (SHOULD NOT)** 除非是关键注意事项，否则避免添加注释；依赖自解释代码
- **C-8 (SHOULD)** 默认使用`type`；仅当更易读或需要接口合并时使用`interface`
- **C-9 (SHOULD NOT)** 除非会在其他地方重用、是单元测试不可测试逻辑的唯一方式，或显著提高不透明块的可读性，否则不要提取新函数

---

### 3 — 测试

- **T-1 (MUST)** 对于简单函数，将单元测试放在与源文件相同目录的`*.spec.ts`中
- **T-2 (MUST)** 对于任何API变更，在`packages/api/test/*.spec.ts`中添加/扩展集成测试
- **T-3 (MUST)** 始终将纯逻辑单元测试与涉及数据库的集成测试分开
- **T-4 (SHOULD)** 优先使用集成测试而非重度模拟  
- **T-5 (SHOULD)** 对复杂算法进行彻底的单元测试
- **T-6 (SHOULD)** 如果可能，在一个断言中测试整个结构
  ```ts
  expect(result).toBe([value]) // 好

  expect(result).toHaveLength(1); // 不好
  expect(result[0]).toBe(value); // 不好
  ```

---

### 4 — 数据库

- **D-1 (MUST)** 将DB助手类型定义为`KyselyDatabase | Transaction<Database>`，使其同时适用于事务和DB实例  
- **D-2 (SHOULD)** 在`packages/shared/src/db-types.override.ts`中覆盖错误的生成类型。例如自动生成的类型显示错误的BigInt值 - 所以我们手动覆盖为`string`

---

### 5 — 代码组织

- **O-1 (MUST)** 只有当代码被≥2个包使用时才放在`packages/shared`中

---

### 6 — 工具门控

- **G-1 (MUST)** 通过`prettier --check`  
- **G-2 (MUST)** 通过`turbo typecheck lint`  

---

### 7 - Git

- **GH-1 (MUST**) 编写提交消息时使用Conventional Commits格式: https://www.conventionalcommits.org/en/v1.0.0
- **GH-2 (SHOULD NOT**) 在提交消息中提及Claude或Anthropic

---

## 编写函数最佳实践

评估你实现的函数是否良好时，使用以下检查清单:

1. 你能阅读该函数并真正轻松地理解它在做什么吗？如果可以，就到此为止
2. 函数是否有很高的圈复杂度？(独立路径数量，或者在许多情况下，作为代理的if-else嵌套数量)。如果有，那么它可能有问题
3. 是否有任何常见的数据结构和算法可以使这个函数更易理解和更健壮？解析器、树、栈/队列等
4. 函数中是否有未使用的参数？
5. 是否有可以移到函数参数中的不必要类型转换？
6. 函数是否容易测试而无需模拟核心功能(如sql查询、redis等)？如果不能，这个函数可以作为集成测试的一部分进行测试吗？
7. 它是否有任何隐藏的未经测试的依赖关系，或者任何可以提取到参数中的值？只关心实际可能改变或影响函数的非平凡依赖关系
8. 头脑风暴3个更好的函数名称，看看当前名称是否最佳，与代码库其余部分一致

重要：除非有强烈需求，否则不应重构出单独的函数，例如:
  - 重构后的函数在多个地方使用
  - 重构后的函数容易单元测试而原始函数不容易且无法通过其他方式测试
  - 原始函数极难理解，你不得不到处添加注释来解释它

## 编写测试最佳实践

评估你实现的测试是否良好时，使用以下检查清单:

1. 应该参数化输入；永远不要直接在测试中嵌入未解释的字面量如42或"foo"
2. 除非测试能因真实缺陷而失败，否则不应添加测试。禁止简单的断言(如expect(2).toBe(2))
3. 应确保测试描述准确说明最终expect验证的内容。如果措辞和断言不匹配，应重命名或重写
4. 应将结果与独立的预先计算的期望值或领域属性进行比较，永远不要将函数的输出重新用作oracle
5. 应遵循与生产代码相同的lint、类型安全和风格规则(prettier、ESLint、严格类型)
6. 应尽可能表达不变量或公理(如交换律、幂等性、往返)而非单一硬编码案例。使用`fast-check`库例如:
```
import fc from 'fast-check';
import { describe, expect, test } from 'vitest';
import { getCharacterCount } from './string';

describe('properties', () => {
  test('concatenation functoriality', () => {
    fc.assert(
      fc.property(
        fc.string(),
        fc.string(),
        (a, b) =>
          getCharacterCount(a + b) ===
          getCharacterCount(a) + getCharacterCount(b)
      )
    );
  });
});
```

7. 函数的单元测试应分组在`describe(functionName, () => ...`下
8. 测试可以是任何值的参数时使用`expect.any(...)`(如变量id)
9. 始终使用强断言而非弱断言，例如`expect(x).toEqual(1)`而非`expect(x).toBeGreaterThanOrEqual(1)`
10. 应测试边界情况、真实输入、意外输入和值边界
11. 不应测试类型检查器能捕获的条件

## 代码组织

- `packages/api` - Fastify API服务器
  - `packages/api/src/publisher/*.ts` - 发布到社交媒体平台的特定实现
- `packages/web` - 使用App Router的Next.js 15应用
- `packages/shared` - 共享类型和工具
  - `packages/shared/social.ts` - 社交媒体平台的字符大小和媒体验证
- `packages/api-schema` - 使用TypeBox的API契约模式

## 记住快捷方式

记住用户可能随时调用的以下快捷方式

### QNEW

当我输入“qnew”时，这意味着：

```
理解CLAUDE.md中列出的所有最佳实践。
您的代码应始终遵循这些最佳实践。
```

### QPLAN
当我输入“qplan”时，这意味着：
```
分析代码库中类似的部分，并确定您的计划是否：
- 与代码库的其余部分一致
- 引入最小的更改
- 重用现有代码
```

## QCODE

当我输入“qcode”时，这意味着：

```
实施您的计划并确保您的新测试通过。
始终运行测试以确保您没有破坏其他任何东西。
始终在新创建的文件上运行 `prettier` 以确保标准格式。
始终运行 `turbo typecheck lint` 以确保类型检查和 linting 通过。
```

### QCHECK

当我输入“qcheck”时，这意味着：

```
您是一位持怀疑态度的资深软件工程师。
对您引入的每个主要代码更改（跳过次要更改）执行此分析：

1. CLAUDE.md清单编写函数最佳实践。
2. CLAUDE.md清单编写测试最佳实践。
3. CLAUDE.md清单实施最佳实践。
```

### QCHECKF

当我输入“qcheckf”时，这意味着：

```
您是一位持怀疑态度的资深软件工程师。
对您添加或编辑的每个主要函数（跳过次要更改）执行此分析：

1. CLAUDE.md清单编写函数最佳实践。
```

### QCHECKT

当我输入“qcheckt”时，这意味着：

```
您是一位持怀疑态度的资深软件工程师。
对您添加或编辑的每个主要测试（跳过次要更改）执行此分析：

1. CLAUDE.md清单编写测试最佳实践。
```

### QUX

当我输入“qux”时，这意味着：

```
想象您是您实现的功能的人类UX测试员。
输出一个您将测试的场景的综合列表，按优先级从高到低排序。
```

### QGIT

当我输入“qgit”时，这意味着：

```
将所有更改添加到暂存区，创建提交，并推送到远程。

编写提交消息时遵循此清单：
- 应使用Conventional Commits格式：https://www.conventionalcommits.org/en/v1.0.0
- 不应在提交消息中提及Claude或Anthropic。
- 应按以下结构组织提交消息：
<type>[可选范围]：<描述>
[可选正文]
[可选页脚]
- 提交应包含以下结构元素以传达意图：
fix：类型为fix的提交修补了代码库中的错误（这与语义版本控制中的PATCH相关）。
feat：类型为feat的提交向代码库引入了新功能（这与语义版本控制中的MINOR相关）。
BREAKING CHANGE：具有页脚BREAKING CHANGE:或在类型/范围后附加!的提交引入了破坏性API更改（与语义版本控制中的MAJOR相关）。BREAKING CHANGE可以是任何类型的提交的一部分。
允许fix:和feat:以外的类型，例如@commitlint/config-conventional（基于Angular约定）推荐build:、chore:、ci:、docs:、style:、refactor:、perf:、test:等。
可以提供BREAKING CHANGE: <description>以外的页脚，并遵循类似于git trailer格式的约定。
