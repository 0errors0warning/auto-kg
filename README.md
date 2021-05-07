# AUTO_KG

# 基于维基百科一键构建知识图谱
## 依赖库
py2neo
BeautifulSoup
lxml
requests
re
gensim
## 运行环境
neo4j desktop,注意直接在浏览器里运行neo4j的可视化的时候要在程序里对登陆路径做出相应的修改
## 基本思想
用深度优先搜索穿过所有类别信息，最后到达实体页面。生成类似树状的结构。
在实体页面，只提取infobox的相关信息，infobox每行左边的元素视为关系名，右边的是要被连接的实体，即该实体的若干属性
## 关于数据清洗
我是懒狗，只把空属性去掉了，没有做补全
考虑到关系意思相似名字不同的情况，使用gensim中的wordvec包生成词向量，余弦相似度高于0.8的合并
未来预计用bert对正文内容做ner，抽取关系等，不过，我是懒狗
## 结构
每个category-xx是一个类,类名就是category-xx，他们之间有子类关系，有infobox的页面是实体，实体名称就是页面标题，infobox里行左侧是关系名，右侧是关系指向的实体
## 输入与输出

### 输入：
以此页面为例
<img width="1269" alt="截屏2021-05-07 下午5 06 09" src="https://user-images.githubusercontent.com/55007360/117426583-9feba180-af56-11eb-8dc1-8c6e483c624d.png">

找到网址，如下
<img width="526" alt="image" src="https://user-images.githubusercontent.com/55007360/117426787-e2ad7980-af56-11eb-9a52-ef4e072a1d78.png">
找到https://www.wanweibaike.com/wiki/ 之后的字样，本例中是Category-第二次世界大战中的欧洲，将该字符串作为scrappy的参数传入，并指定搜索深度即可。

###输出：
在neo4j里就能看到生成的知识图谱,如下：
<img width="1042" alt="image" src="https://user-images.githubusercontent.com/55007360/117439423-6706f900-af65-11eb-837e-cae8d769d16f.png">

## 致谢
在此特别鸣谢我的女友zhb，项目之功共一石，zhb独占十二斗，我倒欠一斗，我写的bug也倒欠一斗
