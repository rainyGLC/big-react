# big-react

学习 react-从 0 实现 React18

## 目的

搭建一个框架

### 搭架子

架子包括：

- 定义项目结构(monorepo)
- 定义开发规(lint、commit、tsc、代码风格)
- 选择打包工具

#### 相关结构

Multi-repo 和 Mono-repo 该如何选择？
Multi-repo 每个库有自己独立的仓库，逻辑清晰，相对应的，协同管理会更繁琐.
Mono-repo 可以很方便的协同管理不同独立的库的生命周期，相对应的，会有更高的操作复杂度

Mono-repo 技术选型
简单工具

- npm workspaces
- Yarn workspaces
- Pnpm workspaces

专业工具

- nx
- bit
- turborepo
- rush
- nx
- lerna

Pnpm 相对其他打包工具的优势：
依赖安装快
更规范(处理幽灵依赖问题)

Pnpm 初始化：
安装

```
1. npm install -g pnpm
2. pnpm init

```

#### 定义开发规范

代码规范检查与修复

- 代码规范：lint 工具
  eslint
  安装

  ```
  1. pnpm i eslint -D -w
  ```

  初始化

  ```
  1. npx eslint --init
  ```

.eslintrc.json 配置如下： //注意，eslint 9.0.0 以上不再支持.eslintrc.json 格式配置文件

```

```

安装 ts 的 eslint 插件

```
1. pnpm i -D -w @typescript-eslint/eslint-plugin
```

代码风格:prettier
安装

```
1. pnpm i  prettier -D -w
```

新建.prettierrc.json 文，添加配置

将 prettier 集成到 eslint 中,其中:
eslint-config-prettier: 覆盖 eslint 本身的规则配置
eslint-plugin-prettier:用 Prettier 来接管修复代码 eslint--fix

为 lint 增加对应的执行脚本，并验证效果

```
1. pnpm i eslint-config-prettier eslint-plugin-prettier -D -w
```

commit 规范检查
安装 husky,用于拦截 commit 命令

```
1. pnpm i husky -D -w
```

初始化

```
1. npx husky install
```

将刚才实现的格式化命令 pnmp lint 纳入 commit 时 husky 将执行的脚本

```
1. npx husky add .husky/pre-commit "pnpm lint"
```

TODO: pnpm lint会对代码全量检查，当项目复杂后执行速度可能比较慢，届时可以考虑使用list-staged来对暂存区的文件进行检查,通过commitlint来对git提交信息进行检查，首先是安装必要的库:

```
1. pnpm i commitlint @commitlint/cli @commitlint/config-conventional -D -w
```

新建配置文件.commitlintrc.js,添加配置如下：

```
module.exports = { extends: ["@commitlint/config-conventional"] };

```

集成到husky中(手动添加commit-msg / pre-commit 钩子，将commitlint添加到其中)

```
1. npx husky add .husky/commit-msg "npx --no-install commitlint --edit $HUSKY_GIT_PARAMS"
```

conventional commit 规范

```
1. //提交的类型：摘要信息
2. // <type>: <subject>
```

常用的type值包括如下:

- feat:添加新功能。
- fix:修复bug。
- chore:一些不影响功能的更改
- docs:文档变更。
- perf:性能优化。
- refactor:重构代码。
- test:添加测试用例。
- style:代码格式（不影响功能，例如空格、分号等格式修正）。

配置tsconfig.json
