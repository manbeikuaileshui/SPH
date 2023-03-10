## 一、分页功能实现

1. 为什么很多项目采用分页功能：比如电商平台同时展示的数据有很多（1万+），采用分页功能
   ElementUI是有相应的分页组件，使用起来超级简单，但是咱们前台项目目前不用（掌握自定义分页功能）

2. 分页器展示，需要哪些数据（条件）？

    需要知道

        pageNo：当前页数

        pageSize：每一页展示的数据条数

        total：一共有多少条数据（一共有多少页也能算出）

        continues：分页器连续的页码个数：5 | 7

3. 自定义分页器，在开发的时候先自己传递假的数据进行调试，调试成功以后在用服务器数据

4. 对于分页器而言，很重要的一个地方即为（算出：连续页面起始数字和结束数字）

例：

    假如页面不够5页：
        则起始数字为1，结束数字为最后一页
    假如页面够5页：以31页为例
        假如当前是第1页，0 -1 1 2 3 ...，修正：起始数字是1，结束数字是5（分页器连续的数字）
        假如当前是第2页，0 1 2 3 4 ...，修正：起始数字是1，结束数字是5（分页器连续的数字）
        假如当前是第3页，1 2 3 4 5 ...，正常：起始数字是1，结束数字是5
        假如当前是第8页，1 ... 6 7 8 9 10 ...，正常：起始数字为6，结束数字为10
        假如当前是第29页，1 ... 27 28 29 30 31 ...，正常：起始数字为27，结束数字为31
        假如当前是第30页，1 ... 28 29 30 31 32 ...，修正：起始数字为27（最后一页 - 分页器连续的数字 + 1），结束数字为31（最后一页）
        假如当前是第31页，1 ... 29 30 31 32 33 ...，修正：起始数字为27（最后一页 - 分页器连续的数字 + 1），结束数字为31（最后一页）

5. 分页器动态展示？分为上中下
v-for可以遍历数组|数字|字符串|对象

6. 开发某一个产品的详情页面？

    （1）静态组件（详情页的组件：还没有注册为路由组件）
        当点击商品图片的时候，跳转到详情页面，在路由跳转的时候需要带上产品的ID给详情页面

    （2）发请求 URL：/api/item{ skuId }  请求方式：get

    （3）vuex 获取商品详情信息
        vuex中还需要新增一个detail模块，需要回到大仓库中合并

    （4）动态展示组件