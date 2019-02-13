---
title: Java中将一个文件夹下所有的文件压缩成一个文件
date: 2018-04-17 12:22:13
tags: Java
---
  	 
	/** 缓冲 */
	static final byte[] buffer = new byte[2048];  


	// 来源  
	File inputDir = new File(request.getServletContext()  
		.getRealPath(Constant.getUploadPath()));  
	if (null != inputDir.listFiles()) {  
	    // 压缩  
	    zip(inputDir.listFiles(), "", zip);  
	}  

<!--more-->
	/** 
	* 压缩ZIP 
	*  
	* @param files 
	*            多个文件 
	* @param baseFolder 
	*            压缩到ZIP的父级目录(目录后面跟上File.separator) 
	* @param zos 
	*            ZipOutputStream 
	* @throws Exception 
	*/  
	private static void zip(File[] files, String baseFolder, ZipOutputStream zos)  
		    throws Exception {  
		// 输入  
		FileInputStream fis = null;  
		// 条目  
		ZipEntry entry = null;  
		// 数目  
		int count = 0;  
		for (File file : files) {  
		    if (file.isDirectory()) {  
			// 递归  
			zip(file.listFiles(),  baseFolder + file.getName() + File.separator, zos);  
			continue;  
		    }  
		    entry = new ZipEntry(baseFolder + file.getName());  
		    // 加入  
		    zos.putNextEntry(entry);  
		    fis = new FileInputStream(file);  
		    // 读取  
		    while ((count = fis.read(buffer, 0, buffer.length)) != -1) {  
			// 写入  
			zos.write(buffer, 0, count);  
		    }  
		    zos.closeEntry(); // 释放资源  
		}  
	}  


	记得用完zip要close掉
