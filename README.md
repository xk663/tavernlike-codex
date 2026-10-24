# SillyTavern Web for Codex

Codex 适配版的酒馆式 LLM 聊天与角色扮演前端开发技能，基于 [ariespo/tavernlike](https://github.com/ariespo/tavernlike)。

适用于 React、Vue 和原生 HTML/JavaScript 项目的接入、修订与排错。保留上游 React 模板和历史参考资料；技能安装不会自动改动你的游戏项目。

## 使用

安装后在 Codex 中输入：

```text
$sillytavern-web 检查当前角色扮演前端，修复提示词组装、停止生成和存档恢复问题，保留现有技术栈。
```

技能默认可自动选择。入口为 `SKILL.md`，界面元数据为 `agents/openai.yaml`。

## 与上游的差异

- Claude Code slash command 改为 Codex `$sillytavern-web`。
- 按需读取参考资料，替代大段内嵌模板和强制问卷。
- 区分新接入和现有项目维护，不再要求批量覆盖文件或自动安装 Dexie。
- 明确取消、重演、回合状态、导入安全、凭据排除与持久化检查。
- 如实说明 React 模板以及旧 Vue/Vanilla 示例的限制，不承诺完整 SillyTavern 兼容。

`templates/` 保留上游代码，未经整套生产验证。已识别限制见 `references/integration.md`。本项目适配的是技能工作流，不宣称已修复全部模板代码。

## 安装

在 Codex 中提供本仓库链接并请求安装根目录技能即可。安装目录名称使用 `sillytavern-web`。

## 来源与许可

上游作者：ariespo。源码固定于 `9d93c5367d9570aa2da9522adb63bfb99156d227`。
上游 README、SKILL.md 和 skill.json 声明 MIT，但该提交未包含独立 LICENSE 文件。保留其原有声明与作者信息，不补造版权年份或许可正文。详见 `NOTICE.md`。
