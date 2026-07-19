# OsirisBuild

自动化每日构建仓库,用于持续编译 [danielkrupinski/Osiris](https://github.com/danielkrupinski/Osiris) 并发布产物。

本仓库**不包含** Osiris 源码,只有一个 GitHub Actions workflow(`.github/workflows/daily-build.yml`)。构建时它会实时拉取上游仓库最新代码,分别用 MSVC / ClangCL 构建出 `Osiris.dll`,再构建出 Linux 的 `libOsiris.so`,一并发布到本仓库的 [Releases](../../releases)。

## 触发方式

- 每天 03:00 UTC 自动运行,若上游没有新提交则跳过
- 手动触发:Actions 页面点 "Run workflow"(可勾选 `force` 强制构建)
- API 触发:
  ```
  curl -X POST -H "Authorization: token <PAT>" \
    https://api.github.com/repos/TIMER-err/OsirisBuild/dispatches \
    -d '{"event_type":"manual-build"}'
  ```

## 使用

去 [Releases](../../releases) 下载对应平台的构建产物,按 [Osiris 原仓库文档](https://github.com/danielkrupinski/Osiris#loading--injecting-into-game-process) 注入使用。

源码、许可与技术细节以上游仓库为准: https://github.com/danielkrupinski/Osiris
