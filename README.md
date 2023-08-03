# vue3-seed-app

* Vue3+Vite4+TypeScript 种子项目框架
* 除了规定了语言和脚手架，还进行了规范配置
* 照搬vue3-element-admin搭建

## 规范配置
### 代码统一规范

[ESLint+Prettier+Stylelint+EditorConfig 约束和统一前端代码规范](https://juejin.cn/post/7241184271318204477 "ESLint+Prettier+Stylelint+EditorConfig 约束和统一前端代码规范")
* Eslint：JavaScript 语法规则和代码风格检查；
* Stylelint: CSS 统一规范和代码检测；
* Prettier：全局代码格式化。
* 需要解决eslint与prettier的冲突  `npm i eslint prettier-eslint eslint-config-prettier --save-dev`

### Git 提交规范
[Husky + Lint-staged + Commitlint + Commitizen + cz-git 配置 Git 提交规范](https://juejin.cn/post/7241562753164230717#heading-3 "Husky + Lint-staged + Commitlint + Commitizen + cz-git 配置 Git 提交规范")
* Husky + Lint-staged 整合实现 Git 提交前代码规范检测/格式化；
* Husky + Commitlint + Commitizen + cz-git 整合实现生成规范化且高度自定义的 Git commit message。

## 整合Pinia
官方文档：[Pinia官方文档](https://pinia.vuejs.org/zh/getting-started.html "Pinia官方文档")

## 环境变量
项目根目录新建 `.env.development` 、`.env.production`
* 开发环境变量配置：.env.development
* 生产环境变量配置：.env.production

**环境变量智能提示**
新建 `src/types/env.d.ts`文件存放环境变量TS类型声明

## vue-router 路由
版本：4.X
文档：[vue router](https://router.vuejs.org/zh/guide/ "Vue Router")

## unplugin 自动导入
> Element Plus 官方文档中推荐 按需自动导入 的方式，而此需要使用额外的插件 unplugin-auto-import  和 unplugin-vue-components  来导入要使用的组件。所以在整合 Element Plus 之前先了解下自动导入的概念和作用

**概念**
为了避免在多个页面重复引入 `API` 或 `组件`，由此而产生的自动导入插件来节省重复代码和提高开发效率。

具体请参考：[unplugin](https://juejin.cn/post/7228990409909108793#heading-7 "unplugin")

**安装插件依赖**
```
npm install -D unplugin-auto-import unplugin-vue-components 
```

**vite.config.ts - 自动导入配置**
```
import AutoImport from "unplugin-auto-import/vite";
import Components from "unplugin-vue-components/vite";

plugins: [
  AutoImport({
    // 自动导入 Vue 相关函数，如：ref, reactive, toRef 等
    imports: ["vue"],
    eslintrc: {
      enabled: true, // 是否自动生成 eslint 规则，建议生成之后设置 false 
      filepath: "./.eslintrc-auto-import.json", // 指定自动导入函数 eslint 规则的文件
    },
    dts: path.resolve(pathSrc, "types", "auto-imports.d.ts"), // 指定自动导入函数TS类型声明文件路径
  }),
  Components({
    dts: path.resolve(pathSrc, "types", "components.d.ts"), // 指定自动导入组件TS类型声明文件路径
  }),
]
```

**.eslintrc.cjs - 自动导入函数 eslint 规则引入**
```
"extends": [
    "./.eslintrc-auto-import.json"
],
```

**tsconfig.json - 自动导入TS类型声明文件引入**
```
{
  "include": ["src/**/*.d.ts"]
}
```


