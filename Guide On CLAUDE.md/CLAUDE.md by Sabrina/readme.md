# AI编码流程
---

### 我的AI编码流程遵循我的CLAUDE.md文件中的步骤：

1. 打开Claude Code（终端或VSCode扩展）
2. 我通常从“正常模式”开始（非规划模式），然后在Claude开始编码时切换到“自动接受编辑模式”
3. 输入 `/clear` 以清除上下文并重新开始
4. 输入 `qnew` 告诉Claude阅读我的CLAUDE.md文件并理解所有最佳实践
5. 与Claude讨论我的用户故事并制定计划，确保尽可能简化，删除不必要的功能或优化，并质疑任何可疑之处
6. 输入 `qplan` 告诉Claude分析代码库中类似的部分，并确定其计划是否：
   1. 与代码库的其余部分一致
   2. 引入最小的更改
   3. 重用现有代码
7. 一旦我对计划满意，我就会输入 `qcode`，它会告诉Claude：

   ```text
   实施您的计划并确保您的新测试通过。
   始终运行测试以确保您没有破坏其他任何东西。
   始终在新创建的文件上运行 `prettier` 以确保标准格式。
   始终运行 `turbo typecheck lint` 以确保类型检查和 linting 通过。
   ```

8. 在Claude开始编写代码后，我经常使用快捷方式 `qcheck`、`qcheckf` 和 `qcheckt`。它们指示Claude审查其代码更改，确保它们符合我CLAUDE.md文件中的最佳实践清单。`qcheckf` 侧重于已添加或更改的函数，而 `qcheckt` 侧重于测试。虽然远非完美，但肯定比没有它好10倍！
9. 我打开工作树并查看Claude对文件的实时编辑，这样我就可以跟踪它的思维过程和它提出的更改。我寻找以下内容：
   1. 面条式代码，即不易理解的代码块
   2. 对API或后端功能的重大更改
   3. 不必要的导入、函数、注释等。
10. 当我对代码满意时，我输入 `qux`，它会告诉Claude：

    ```text
    想象您是您实现的功能的人类UX测试员。
    输出一个您将测试的场景的综合列表，按优先级从高到低排序。
    ```

    这非常有用，因为它会输出一个像这样的UX测试列表，我将逐一测试：

    ![Image](https://substackcdn.com/image/fetch/$s_!o6mg!,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fe49c5ca4-e001-4188-bb5b-5d8198cf7cdf_580x780.png)

11. 最后一步是提交更改并推送。我输入 `qgit`，Claude Code会按照Conventional Commits格式编写一个漂亮的提交消息。
在YouTube视频中，我将逐步完成这个完整的流程，在我的代码库中实现一个真实的功能。在此观看：[YouTube视频](https://www.youtube.com/watch?v=SDiDkK0r-9c)

---

#### 逐步讲解包含AI编码规则的CLAUDE.md文件，然后从头开始实现一个真实的功能，遵循结构化的分步流程。

#### 亲身参与，反驳AI计划，阻止其误入歧途，质疑代码，并进行广泛测试。

所有功劳归于 [sabrina.dev](https://www.sabrina.dev/p/ultimate-ai-coding-guide-claude-code) 分享他们的工作。


## 终端中可能显示的效果：

<img width="1166" height="783" alt="{8479395A-E4B1-4A49-8AF3-1C87ADE3659C}" src="https://github.com/user-attachments/assets/d792ef1e-5e7d-4ac0-b8e8-c0e9e03a0087" />

<img width="1137" height="1242" alt="{E133C2C3-F2AB-4836-91A7-E1F4F373D1DD}" src="https://github.com/user-attachments/assets/db8f4d03-2aa0-4aeb-bfb4-090f84bd38c4" />





