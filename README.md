# Css Moudle Test(version - 0.0.1)
===========================================================================================

##【目录结构】
 \static9\pub\flagment:
    ---
     |---- basic/               不同的base.css文件提供选择(模块的基础，所有样式均基于它)
     |---- grid/                模块外层框架，栅格系统，样式统一使用 grid 表示样式名
     |---- modules/				具体的模块文件，目录名即模块名[每个模块必须提供对应html文件，以及预览图片]
     |---- pages/               用模块拼装的完整页面
     |---- ui/					碎片化组件，可以直接嵌入模块
     |---- READEME.txt

##【模块目的】
* 将页面以块为单位划分为不同模块，每个模块单独写样式，一个模块一个css文件；
  编辑在后台可以选择模块自行搭建页面，模块本身可以有简单配置项(比如文字行数控制，皮肤等)；
  公司统一规范，节约成本；


##【模块规则】
* 1) base + modules + [页面inline css(可选)] （模块ID + 所有碎片版本号）-> MD5
* 2) 每个页面最多2个css文件: a) 一个头尾公用包含全局共用，b) 页面级模块css文件 （这个地方得看css怎么合并了，也许会有变化）
* 3) 静态资源放在static9下面，页面css里面使用绝对路径<aplus cms 负责将版本号替换成正式的>，如：http://static9.pplive.cn/pptv/pub/v_20130608151705/css/sprite.png
* 4) 将页面按模块划分，一个模块一个css文件夹
* 5) 模块以module-* 开头的文件(夹)，模块是由组件(ui-*)组成
* 6) 模块本身的一些交互态在外层添加class完成，如：module-name-hover, module-name-active
* 7) 定义好文件命名规则，文件名就是模块名，如：module-pagelist
* 8) 每做好一个css模块后，必须有想对应的预览图以及对应的html代码
* 9) css 模块作者，注释和后续模块修改记录都可以在css文件中加注释，文件合并的时候会忽略这些
* 10) 每个模块开发的时候，尽量要到自适应，不限制高宽 - 高度可以通过后台简单配置，宽度可以通过外层框架控制
    ```例如：
    /**
     * @author 	Erick Song
     * @date 	2013-03-02
     * @email	ahschl0322@gmail.com
     * @info    网站播放页样式
     */
    ```
* 11) 写模块的时候尽量不要指定某些特定标签来写样式，最好使用class来控制，这样后续更换成其他标签也可以
    ```例如：
    一个按钮可以用 button, span, a等
    ```
11) 页面拼装模块的时候，每个模块上加一个唯一class命名，如module-skin-*【适应编辑需求，页面覆写】


##【前缀占用】
* 1) 终端识别 plt-*           <限制在body中使用，后端输出>
* 2) 栅格系统 grid-*
* 3) 模块标识 module-*
* 4) 组件标识 ui-*
* 5) 按钮标识 btn-*
* 6) 全局标识 g-* 或 g_*      <g_ 为原有头尾模块>


##【模块命名规则】
* 1) 尽量让人看到名字就能知道是什么模块，如module-photoslide
* 2) 模块状态：(hover, active[current], selected, disabled, focus, blur, checked, success, error)
	```module-name-hover, module-name-active```


##【模块限制性命名】
* 1) 栅格系统以及模块框架中定义的class，页面级不要轻易使用，比如:
    栅格：      grid
    模块：      module以及hd, bd, ft

* 2) 终端判断标识class - plt-*
    网站：      plt-web
    客户端：    plt-clt
    多终端：    plt-sm
    (待补充)...


##【模块对应模块名】
* module-test     测试demo
  module-slider   标准slider，全站通用
  module-picshow  带有标题及tab的通用图片展示模块


##【模块写法约定与建议】
* 1) 尽量保证html格式规范，让一个完整的div标签的开头和结尾缩进在同一列，保证页面代码可读性
* 2) 模块里面的标签样式尽量不要使用一些通用样式，如nav之类，这样很容易和其他样式冲突，可以考虑使用模块名作为前缀，如：
    ```html
     <div class="module-slider cf">
        <div class="slider-viewer">
            <ul class="slider-focus">
                <li>
                    <a class="slider-img" href="http://v.pptv.com/show/3RhGxCySAkAsqhI.html" title="天龙八部" target="_blank">
                        <img src="http://img1.pplive.cn/images/2013/06/07/10343559456.jpg" data-src="http://img1.pplive.cn/images/2013/06/07/10343559456.jpg" alt="超人：钢铁之躯">
                    </a>
                    <p class="slider-txt">
                        <a href="http://v.pptv.com/show/3RhGxCySAkAsqhI.html" title="《天龙八部》菜鸟记者陈意涵卷入网络暴动，技术男陈柏霖追查幕后黑手" target="_blank">
                            <strong>复仇者联盟重磅出击</strong>
                            <span>据台湾媒体报道，马英九对菲律宾枪杀台湾渔</span>
                        </a>
                        <span class="slider-bg"></span> <!-- 背景可以用i来处理 -->
                    </p>
                </li>
            </ul>
        </div>
    </div>
    ```
* 3) ...

```
/**
 * 页面是以模块为单位，但是模块继承或限定于栅格-grid系统使用
 * ==========================================================
 * 简单的模块设计: <这个地方有点纠结，是否需要module这个层级，或者说是不是可以和grid合并到一起？>
 * 模块本身有一个mod通用class，这个全局控制，然后紧跟一个模块本身样式 如module-slider，在加一个可配置class cf - 清除浮动
 * <div class="grid">
 *  <div class="module">
 *      <div class="m cf">
 *          <!-- 每个模块本身通过style写高度，这个高度严格参考产品文档或设计稿 -->
 *          {{#include module 碎片}}</div>
 *      <div class="s cf">{{#include module 碎片}}</div>
 *  </div>
 * </div>
 *
 * 广告模块设计：<默认所有广告模块初始化没有高度，广告加载完成后出现高度>
 * <div class="grid">
 *  <div class="sp sp_200116"></div>
 * </div>
 */
```

##【标准模块 module-*】
* 一个标准模块由三个部分组成(简单模块可以选择忽略hd, bd, ft 但是必须有外层module)：
    ```html
    <div class="module-A module-A-hover">
        <div class="hd">
            <h2 class="module-title">{{module-title}}</h2>
        </div>
        <div class="bd">
            {{module-body}}
        </div>
        <div class="ft">
            {{module-footer}} /*include ui-page-list*/
        </div>
    </div>
    ```


    ```
    html
    <div class="module-B">
    	<div class="ui-box">
    	    <div class="ui-box-head">
    	        <div class="ui-box-head-border">
    	            <h3 class="ui-box-head-title">区块标题</h3>
    	        </div>
    	    </div>
    	    <div class="ui-box-container"></div>
    	</div>
    </div>
    ```


##【模块组件 ui-*】
```html
<div class="ui-box ui-box-hover">
    <div class="ui-box-head">
        <div class="ui-box-head-border">
            <h3 class="ui-box-head-title">区块标题</h3>
        </div>
    </div>
    <div class="ui-box-container"></div>
</div>
```


##【合并与发布】
* 页面搭建完毕后，发布前会完成页面模块解析，分析页面所需模块，动态合并css文件；

* 合并发布建议：
    //文件合并可以参考下面这样，方便调试 - page-play.min.css
    (页面解析动态模块依赖 http://static9.pplive.cn/pub/styles/ + 'module path')
    @import 'module-a.css';
    @import 'module-b.css';
    @import 'module-c.css';

* //page.css
    .test{
    	font-size : 12px;
    	color : '#f00';
    }



## 草稿：
==================================================================
#［reset + base(基于pplive-ui) + moudles + page css(模块差异化)］
# base + modules + 页面inline css
