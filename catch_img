<?php

/**
 * 保存图片方法
 * @param [type] $url   远程图片的完整URL地址，不能为空。
 * @param string $filename 文件名 可选变量
 */
function GrabImage($url,$filename="") {
   //不指定文件名
   if($filename=="")
   {
     $ext=strrchr($url,".");
     $filename=time().rand(0,999).$ext;
   }
   ob_start();
   readfile($url);
   $img = ob_get_contents();
   ob_end_clean();
   $destination_folder = './Download/'; // 下载的文件保存目录。必须以斜杠结尾 
	if(!is_dir($destination_folder))
	{
		//若无则创建，并给与777权限 windows忽略  //判断目录是否存在 
		mkdir($destination_folder,0777);
	} 
   $size = strlen($img);
   $fp2=@fopen($destination_folder.$filename, "a");
   fwrite($fp2,$img);
   fclose($fp2);
   return $filename;
}


/**
* 从html内容中筛选链接
*
* @param string $web_content
* @return array
*/
function _filterUrl($web_content){
	$reg_tag_a ="/<[img|IMG].*?src=[\'|\"](.*?(?:[\.gif|\.jpg]))[\'|\"].*?[\/]?>/";
	$result = preg_match_all($reg_tag_a,$web_content,$match_result);
	if($result)
	{
		return $match_result[1];
	}
}


/**
* 测试
*/
function main(){
	$url = 'http://www.nipic.com/';
	$handle = fopen($url, "r");
	if($handle)
	{
		$content = stream_get_contents($handle,1024*1024);
		$result =  _filterUrl($content); //获取到图片的url
		//var_dump($result);
		foreach ($result as $key => $value) {
			$a = GrabImage($value);
			var_dump($a);
		}
	}else
	{
		return false;
	}	

}

main();
