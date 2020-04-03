###命名规则
- 版本号 + 功能名称
- 功能名称尽量( 非强制 )少于 3 个单词描述, 单词之间用下划线 `_ ` 分割

###示例
```
feature/1.0.0_version_update
bugfix/1.0.0_match_ui
```

#### master 分支
主分支, 用于发布到生产环境的代码, 不能在这个分支上面直接提交修改

#### develop 分支
开发主分支,  主要合并 `feature` 、 `bugfix` 、  `release`  分支

#### release 分支
`feature` 分支开发完毕, 合入 `develop` 分支, 基于 `develop` 分支创建一个新的 `release` 分支, 用于提测, 这个阶段所有的 bug 修复都合并到这个分支,  测试完毕后重新合入 `develop` 和 `master`

#### feature 分支
根据需求划分功能点创建的分支,  尽可能保证一个需求点一个分支 （!!#ff9900 非强制!!）

#### bugfix 分支
提测期间 bug 修改所在的分支、或者线上 bug 修复

#### merge request
`feature` 分支开发完毕后, 在 gitlab 网页端发起 merge request 合入 `develop` 分支,  并 @ 1~2个小伙伴 review 代码, 有问题及时修改, 重复上述工作直至没有问题再合入

#### 提交记录格式
- 英文单词、数字 前后与中文留一个空格位置
- 【Feature】 完成 xxx 功能 ；
- 【Feature】 完成 xxx 模块 UI ；
- 【Feature】 完成 xxx 架构搭建 ；
- 【Optimize】 优化 UITableView 滑动速度
- 【Bugfix】#669 修复 xxx 问题 （带上 bug 编号方便测试查看提交记录）

以上提交格式非强制,  只要能保证记录清晰即可, 最好不要出现随意数字、英文、中文等内容不明的情况


#### 注意事项
- `develop` 分支及时更新,  自己的 `feature` 分支每天及时执行 rebase `develop` 分支操作, 避免之后合并代码出现太多冲突
-  （!!#ff9900 强制!!）封包之后及时出 tag ，在此期间如果不是严重 bug， 禁止再更新代码

