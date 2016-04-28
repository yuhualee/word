
### 安装

* 安装gulp

	```
	npm install gulp -g   //安装
	cd 目录
	npm install gulp --save-dev
	```
	> 上述指令将gulp安装到本地端的专案内，并纪录于package.json内的devDependencies物件。请确保目录里面含有package.json。
	
### gulp模块的方法

* **gulp.src()** -- 输入

	gulp模块的src方法，用于产生数据流。它的参数表示所要处理的文件，这些指定的文件会转换成数据流。

	```
	js/app.js：指定确切的文件名。
	js/*.js：某个目录所有后缀名为js的文件。
	js/**/*.js：某个目录及其所有子目录中的所有后缀名为js的文件。
	!js/app.js：除了js/app.js以外的所有文件。
	*.+(js	css)：匹配项目根目录下，所有后缀名为js或css的文件
	```
	src方法的参数还可以是一个数组，用来指定多个成员。
	
	```
	gulp.src(['js/**/*.js', '!js/**/*.min.js'])
	```
	
* **gulp.dest()** -- 输出

	dest方法将管道的输出写入文件，同时将这些输出继续输出，所以可以依次调用多次dest方法，将输出写入多个目录。如果有目录不存在，将会被新建。


* **.pipe()** -- 管道

* **gulp.task()** -- 任务

	task方法用于定义具体的任务。它的第一个参数是任务名，第二个参数是任务函数
	
	```
	gulp.task('color',function(){
		console.log('green');
	});
	```
	```
	gulp color    //启动任务
	```
	
	task方法还可以指定按顺序运行的一组任务。
	
	```
	gulp.task('build', ['css', 'js', 'imgs']);
	```
	> 上面代码先指定build任务，它由css、js、imgs三个任务所组成，task方法会并发执行这三个任务。
	
	如果希望各个任务严格按次序运行，可以把前一个任务写成后一个任务的依赖模块。
	
	```
	gulp.task('css', ['greet'], function () {
   		// Deal with CSS here
	});
	```
	
	> 上面代码表明，css任务依赖greet任务，所以css一定会在greet运行完成后再运行。
	
	**如果一个任务的名字为default，就表明它是“默认任务”，在命令行直接输入gulp命令，就会运行该任务。**
	
	```
	gulp.task('default', ['styles', 'jshint', 'watch']);
	```
	> 执行的时候，直接使用gulp，就会运行styles、jshint、watch三个任务。
	
	
* **gulp.watch()** -- 监视

	watch方法用于指定需要监视的文件。一旦这些文件发生变动，就运行指定任务。
	
	```
	gulp.task('watch',function(){
		gulp.watch('app/scripts/*.js', ['guglify']);
	});
	```

* **gulp命令**
	
	```
	gulp.task(name[, deps], fn);  //定义任务 name: 任务名称， deps：依赖任务名称   fn: 回调函数
	gulp.run(tasks...); //尽可能多的并行执行多个task
	gulp.watch(glob,fn);  //当glob内容发生改变时，执行fn
	gulp.src(glob);    //置需要处理的文件的路径，可以是多个文件以数组的形式，也可以是正则
	gulp.dest(path[,options]);   //设置生成文件的路径
	```
		> gulp将要处理的文件通过管道(pipe())API导向相关插件，通过插件执行文件的处理任务。
		
### gulp插件
	
* 安装外挂
	
	* 编译Sass (gulp-ruby-sass)
	* Autoprefixer (gulp-autoprefixer)
	* 缩小化(minify)CSS (gulp-minify-css)
	* JSHint (gulp-jshint)
	* 拼接 (gulp-concat)
	* 丑化(Uglify) (gulp-uglify)
	* 图片压缩 (gulp-imagemin)
	* 即时重整(LiveReload) (gulp-livereload)
	* 清理档案 (gulp-clean)
	* 图片快取，只有更改过得图片会进行压缩 (gulp-cache)
	* 更动通知 (gulp-notify)
	* 自动加载package.json里面的所有gulp插件  (gulp-load-plugins)
		
		```
		npm install gulp-ruby-sass --save-dev
		```
		
* 载入外挂
	
	```
	var gulp = require('gulp'),
		sass = require('gulp-ruby-sass'),
		autoprefixer = require('gulp-autoprefixer'),
		minifycss = require('gulp-minify-css'),
    	jshint = require('gulp-jshint'),
    	uglify = require('gulp-uglify'),
	    imagemin = require('gulp-imagemin'),
   		rename = require('gulp-rename'),
    	clean = require('gulp-clean'),
	    concat = require('gulp-concat'),
	    notify = require('gulp-notify'),
   		cache = require('gulp-cache'),
	    livereload = require('gulp-livereload');
	```
				
	* 建立任务
	
		```
		gulp.task('mytask', ['array', 'of', 'task', 'names'], function() {
			// Do stuff
		});
		```
	
		```
		gulp.task('style',function(){
			return gulp.src('src/styles/*.scss'), 
				.pipe(gulp.dest('dist/assets/css'));  
		});
		```
		
		> 1. 用来建立任务，可通过终端`gulp styles`来执行   
		> 2. `gulp.src`用来定义一个或多个来源档案，多个来源用*匹配。
		> 3. 使用`pipe()`来串流来源档案到某个外挂，串流(stream)让它成为非同步机制，所以在我们收到完成通知之前，确保该任务全部完成。
		> 4. `gulp.dest(path[,options])` 设定目标的路径，可以有多个目的地，
		
* **gulp-load-plugins** - 从package.json里加载所有依赖的gulp插件
		
	```
	npm install --save-dev gulp-load-plugins
	```
		
	```
	var gulp = require('gulp');
	var gulpLoadPlugins = require('gulp-load-plugins');
	var plugins = gulpLoadPlugins();
	```
	相当于如下结果：
		
	```
	plugins.jshint = require('gulp-jshint');
	plugins.concat = require('gulp-concat');
	```


#### css处理


* **sass编译及压缩**

	```
	gulp.task('sass',function(){
		return gulp.src('src/styles/*.scss')
			.pipe(sass({style: 'compressed'}))
			.pipe(autoprefixer('last 2 version','safari 5'))
			.pipe(gulp.dest('dist/assets/css'))
	});
	```


* **gulp-autoprefixer**

	autoprefixer 解析 CSS 文件并且添加浏览器前缀到CSS规则里。 通过示例帮助理解
	
	处理前：
	
	```
	.demo{
		display:flex;
	}
	```
	
	处理后：
	
	```
	.demo {
    	display:-webkit-flex;
	    display:-ms-flexbox;
    	display:flex;
	}
	```
	
	```
	var gulp = require('gulp'),
    autoprefixer = require('gulp-autoprefixer');
	gulp.task('testAutoFx', function () {
    	gulp.src('src/css/index.css')
        	.pipe(autoprefixer({
            	browsers: ['last 2 versions', 'Android >= 4.0'],
	            cascade: true, //是否美化属性值 默认：true 像这样：
    	        //-webkit-transform: rotate(45deg);
        	    //        transform: rotate(45deg);
            	remove:true //是否去掉不必要的前缀 默认：true 
	        }))
    	    .pipe(gulp.dest('dist/css'));
	});
	```
	
	> 你只需要关心编写标准语法的 css，autoprefixer 会自动补全。
	
* **gulp-minify-css**

	```
	gulp.task('minify',function(){
		return gulp.src('app/css/*.scss')
		.pipe(sass())
		.pipe(minifyCss())
		.pipe(gulp.dest('dist/css/'))
	});
	```

* **综合处理**

	```
	gulp.task('styles',function(){
		return gulp.src('app/css/*.scss')   //选择文件
		.pipe(sass({style:'expanded'}))    //sass编译
		.pipe(autoprefixer({}))   //自动扩展浏览器兼容性
		.pipe(gulp.dest('dist/css/*.css'))    //输出
		.pipe(rename({suffix:'.min'}))   //重命名
		.pipe(gulp.dest('dist/css/*.css'))   //输出
		.pipe(concat())    //合并css
		.pipe(minifycss())   //压缩
		.pipe(gulp.dest('dist/css/*.css'))   //输出
	});	
	```


#### js处理


	
* JSHint，拼接及压缩

* **综合**

	```
	gulp.task('scripts',function(){
		return gulp.src('app/scripts/*.js')
		.pipe($.jshint())
		.pipe($.concat('all.js'))
		.pipe(gulp.dest('dist/scripts'))   //合并后的文件
		.pipe($.uglify())   //压缩后文件
		.pipe($.rename({suffix:'.min'}))    //重命名,如果没有这一步，将覆盖原文件
		.pipe(gulp.dest('dist/scripts'))   //输出
	});	
	```

#### 图片处理

* **gulp-imagemin:** 压缩图片

* **gulp-cache:** 只压缩修改的图片，没有修改的图片直接从缓存文件读取


	压缩图片文件（包括PNG、JPEG、GIF和SVG图片）


	```
	var imagemin = require('gulp-imagemin');
	var cache = require('gulp-cache');
	gulp.task('images',function(){
		return gulp.src('app/images/**/*')
		.pipe(cache(imagemin({
            optimizationLevel: 5, //类型：Number  默认：3  取值范围：0-7（优化等级）
            progressive: true, //类型：Boolean 默认：false 无损压缩jpg图片
            interlaced: true, //类型：Boolean 默认：false 隔行扫描gif进行渲染
            multipass: true //类型：Boolean 默认：false 多次优化svg直到完全优化
        }))))
		.pipe(gulp.dest('dist/images'))
	});	
	```
#### html处理

* **gulp-htmlmin：**

	```
	gulp.task('htmls',function(){
		var options = {
        	removeComments: true,//清除HTML注释
	        collapseWhitespace: true,//压缩HTML
    	    collapseBooleanAttributes: true,//省略布尔属性的值 <input checked="true"/> ==> <input />
        	removeEmptyAttributes: true,//删除所有空格作属性值 <input id="" /> ==> <input />
	        removeScriptTypeAttributes: true,//删除<script>的type="text/javascript"
    	    removeStyleLinkTypeAttributes: true,//删除<style>和<link>的type="text/css"
        	minifyJS: true,//压缩页面JS
	        minifyCSS: true//压缩页面CSS
    	};
	    gulp.src('src/html/*.html')
    	    .pipe($.htmlmin(options))
        	.pipe(gulp.dest('dist/html'));
	});
	```

	> [参考](https://github.com/kangax/html-minifier#user-content-options-quick-reference)

#### 后期处理

* **gulp-livereload** - 自动刷新浏览器

	当监听文件发生变化时，浏览器自动刷新页面。【事实上也不全是完全刷新，例如修改css的时候，不是整个页面刷新，而是将修改的样式植入浏览器，非常方便。】特别是引用外部资源时，刷新整个页面真是费时费力。
	
	安装：

	```
	npm install gulp-livereload --save-dev
	```
	配置：
	
	```
	var sass = require('gulp-sass');
	var livereload = reqiure('gulp-livereload');
	gulp.task('styles',function(){
		return gulp.src('app/styles/*.scss')
		.pipe(sass())   //sass编译
		.pipe(gulp.dest('dist/styles'))   //输出
		.pipe(livereload())    //自动刷新
	});
	gulp.task('watch',function(){
		livereload.listen();
		gulp.watch('app/styles/*.scss',['styles']);
	});
	```


* **gulp-rev-append**  清除缓存

	安装

	```
	npm install gulp-rev-append --save-dev
	```
	
	使用：
	
	```
	var gulp = require('gulp'),
    rev = require('gulp-rev-append');
	gulp.task('testRev', function () {
    	gulp.src('src/html/index.html')
        .pipe(rev())
        .pipe(gulp.dest('dist/html'));
	});
	```


* **gulp-clean** - 收拾干净

	```
	gulp.task('clean', function() { 
  		return gulp.src(['dist/assets/css', 'dist/assets/js', 'dist/assets/img'], {read: false})
    		.pipe(clean());
	});
	```	
	> 我们可以传入一个目录(或档案)阵列到gulp.src。因为我们不想要读取已经被删除的档案，我们可以加入read: false选项来防止gulp读取档案内容–让它快一些。
	
* 预设任务

	```
	gulp.task('default',['clean'],function(){
		gulp.start('styles','scripts','images');
	})
	```
	
	> gulp.start开始任务前会先执行清理`clean`,确定clean执行完成后，然后并行执行里面的任务。

* 看守

	```
	gulp.task('watch',function(){
		//看守所有的.scss档
		gulp.watch('src/styles/**/*.scss',['styles']);
		gulp.watch('src/scripts/**/*.js',['scripts']);
		gulp.watch('src/images/**/*',['images']);
	});
	```
	
	> 透过gulp.watch指定想要看守的档案，并且透过相依任务阵列定义任务。执行$ gulp watch来开始看守档案，任何.scss、.js或图片档案一旦有了更动，便会执行相对应的任务。
	
	
* **gulp-useref**

	```
	var gulp = require('gulp'),
    useref = require('gulp-useref');
	gulp.task('default', function () {
    	return gulp.src('app/*.html')
        	.pipe(useref())
	        .pipe(gulp.dest('dist'));
	});
	```
	
	如果你想让它再进行其它修改，可以使用gulp-if去有条件的处理。
	
	```
	var gulp = require('gulp'),
    useref = require('gulp-useref'),
    gulpif = require('gulp-if'),
    uglify = require('gulp-uglify'),
    minifyCss = require('gulp-minify-css');
	gulp.task('html', function () {
    	return gulp.src('app/*.html')
        	.pipe(useref())
	        .pipe(gulpif('*.js', uglify()))
    	    .pipe(gulpif('*.css', minifyCss()))
        	.pipe(gulp.dest('dist'));
	});
	```
	
	html
	
	```
	<!-- build:<type>(alternate search path) <path> <parameters> -->
	... HTML Markup, list of script / link tags.
	<!-- endbuild -->
	```
	
	例如：
	
	```
	<html>
	<head>
    	<!-- build:css css/combined.css -->
	    <link href="css/one.css" rel="stylesheet">
    	<link href="css/two.css" rel="stylesheet">
	    <!-- endbuild -->
	</head>
	<body>
    	<!-- build:js scripts/combined.js -->
	    <script type="text/javascript" src="scripts/one.js"></script>
    	<script type="text/javascript" src="scripts/two.js"></script>
	    <!-- endbuild -->
	</body>
	</html>
	```
	result:
	
	```
	<html>
	<head>
    	<link rel="stylesheet" href="css/combined.css"/>
	</head>
	<body>
    	<script src="scripts/combined.js"></script>
	</body>
	</html>
	```

* **opn**

	```
	npm install --save-dev opn
	```

	
---
	

* **watchPath(event, search, replace, distExt)**

	参数     |	说明
	--------|-------------------------
	event   |  gulp.watch 回调函数的 event
	search	 |  需要被替换的起始字符串
	replace  | 	第三个参数是新的的字符串
	distExt  | 	扩展名(非必填)	
	
	