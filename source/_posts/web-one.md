---
title: web笔记一
date: 2020-06-15 14:56:44
tags: [web]
categories: [web]
meta:
  header: [title, author, category,date,wordcount]
---
## 文件上传功能

<!-- more -->

### 前端
```
<div style={{marginTop: 30, marginBottom: 20,width:'50%',marginLeft: 20}}>
                        <span style={{display: 'inline-block', width: 150}}> <Icon type="to-top"/>上传单个文件</span>
                        <Upload
                            name="file"
                            action="http://localhost:8080/upload"
                            /*onChange = {this.handleChange}
                             onRemove = {this.remove}*/>
                            <Button>
                                <Icon type="upload" /> Click to Upload
                            </Button>
                        </Upload>
                    </div>

                    <div style={{marginTop: 30, marginBottom: 20,width:'50%',marginLeft: 20}}>
                        <span style={{display: 'inline-block', width: 150}}> <Icon type="to-top"/>上传多个文件</span>
                        <Upload
                            name="file"
                            action="http://localhost:8080/multiUpload"
                            multiple={true}
                            /*onChange = {this.handleChange}
                             onRemove = {this.remove}*/>
                            <Button>
                                <Icon type="upload" /> Click to Upload
                            </Button>
                        </Upload>
                    </div>
```
### 服务端

#### 单文件上传
```
@PostMapping("/upload")
    @ResponseBody
    public String upload(@RequestParam("file") MultipartFile file) {
        if (file.isEmpty()) {
            return "上传失败，请选择文件";
        }

        try {
            String fileName = file.getOriginalFilename();
            File directory = new File(".");
            String filePath = directory.getCanonicalPath() + "\\src\\main\\resources\\files\\";
            File dest = new File(filePath + fileName);
            file.transferTo(dest);
            System.out.println("success");
            return "上传成功";
        } catch (IOException e) {
            System.out.println("fail");
        }
        return "上传失败！";
    }
```
#### 多文件上传
```
@PostMapping("/multiUpload")
    @ResponseBody
    public String multiUpload(HttpServletRequest request) {
        List<MultipartFile> files = ((MultipartHttpServletRequest) request).getFiles("file");
        File directory = new File(".");
        String filePath = null;
        try {
            filePath = directory.getCanonicalPath() + "\\src\\main\\resources\\files\\";
        } catch (IOException e) {
            e.printStackTrace();
            return "error";
        }
        for (int i = 0; i < files.size(); i++) {
            MultipartFile file = files.get(i);
            if (file.isEmpty()) {
                return "上传第" + (i++) + "个文件失败";
            }
            String fileName = file.getOriginalFilename();

            File dest = new File(filePath + fileName);
            try {
                file.transferTo(dest);
                System.out.println("第" + (i + 1) + "个文件上传成功");
            } catch (IOException e) {
                System.out.println(e.toString());
                return "上传第" + (i++) + "个文件失败";
            }
        }

        return "上传成功";
    }
```