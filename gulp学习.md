
* 安装gulp

	```
	npm install gulp -g   //安装
	cd 目录
	npm install gulp --save-dev
	```
	> 上述指令将gulp安装到本地端的专案内，并纪录于package.json内的devDependencies物件。请确保目录里面含有package.json。

	* **gulp命令**
	
		```
		gulp.task(name[, deps], fn);  //定义任务 name: 任务名称， deps：依赖任务名称   fn: 回调函数
		gulp.run(tasks...); //尽可能多的并行执行多个task
		gulp.watch(glob,fn);  //当glob内容发生改变时，执行fn
		gulp.src(glob);    //置需要处理的文件的路径，可以是多个文件以数组的形式，也可以是正则
		gulp.dest(path[,options]);   //设置生成文件的路径
		```
		> gulp将要处理的文件通过管道(pipe())API导向相关插件，通过插件执行文件的处理任务。
	
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
			npm install gulp-ruby-sass
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
		
		**gulp-load-plugins** - 从package.json里加载所有依赖的gulp插件
		
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
		> 3. 使用pipe()来串流来源档案到某个外挂，串流(stream)让它成为非同步机制，所以在我们收到完成通知之前，确保该任务全部完成。
		> 4. `gulp.dest(path[,options])` 设定目标的路径，可以有多个目的地，

* sass编译及压缩

	```
	gulp.task('sass',function(){
		return gulp.src('src/styles/*.scss')
			.pipe(sass({style: 'compressed'}))
			.pipe(autoprefixer('last 2 version','safari 5'))
			.pipe(gulp.dest('dist/assets/css'))
	});
	```
	
* JSHint，拼接及压缩

* 图片压缩

* 收拾干净

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
	
* 即时重整

	Gulp也可以处理档案更动后，自动重新整理页面。我们需要修改watch任务，设置即时重整伺服器。


		```
		gulp.task('watch',function(){
		
			//建立即时重整服务器
			var server = livereload();
			
			// 看守所有位在 dist/  目录下的档案，一旦有更动，便进行重整
			gulp.watch(['dist/**']).on('change', function(file){
    			server.changed(file.path);
				
			});
		})
		```



* **gulp-uglify**

	```
	gulp.task('compress',function(){
		return gulp.src('app/scripts/*.js')
		.pipe(uglify())
		.pipe(gulp.dest('dist'))
	});	
	```



	

	
	
* 参考

	[gulp API](https://github.com/gulpjs/gulp/blob/master/docs/API.md);
	[jshint](http://jshint.com/docs/reporters/)
	[gulp](http://javascript.ruanyifeng.com/tool/gulp.html)