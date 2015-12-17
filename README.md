PHP5.5以上路由

安装

	composer require sunkangchina/php-router dev-master
	

路由说明

	Route::get('/','site'); //路由到Controllers\Site类中的indexAction方法
	Route::get('a','home/site@index'); // //路由到Modules\Home\Site类中的indexAction方法


 	

执行路由
	
	try {  
		$view = Route::run();  
		if($view){
			echo $view;
			$time_end = microtime(true);
			$used = number_format($time_end - $time_start,2);
			echo "\n<!--total used time:". $used.'s-->';
		}
	}catch (Exception $e) {  
		dump($e->getMessage()); 
	} 


 

生成URL

	echo Route::create_url('post',['id'=>1,'d'=>3]);
	

二级域名路由

	
	Route::domain('user2.api.com',function(){
		Route::get('/',function(){
			echo 111;		
		});

		Route::get('test',function(){
			echo 'test';		
		});
	});
	
	 
多条规则路由

	Route::get('post/<id:\d+>|post',function(){    
	},'@post');
	
	Route::get('post/<id:\d+>|post',function(){    
	},'@post|$po');
	



apache	.htaccess 配置 


	 RewriteEngine On 
	 RewriteCond %{REQUEST_FILENAME} !-d
	 RewriteCond %{REQUEST_FILENAME} !-f
	 RewriteRule ^ index.php [L]

 
 
 