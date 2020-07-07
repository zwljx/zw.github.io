---
title: Java笔记一
date: 2020-07-07 18:11:40
tags: [java]
categories: [java]
meta:
  header: [title, author, category,date,wordcount]
---
## 文件工具类

<!-- more -->

```
import org.apache.commons.lang3.StringUtils;

import java.io.*;
import java.util.ArrayList;
import java.util.List;


public class FileUtil {
    /**
     * 按行读取文件，一行为一个String
     * @param path filePath
     * @return
     */
    public static List<String> readFile(String path){
        List<String> result = new ArrayList<String>();
        FileReader reader = null;
        try {
            reader = new FileReader(path);

            BufferedReader br = new BufferedReader(reader);
            String str = null;
            while ((str = br.readLine()) != null) {
                if(StringUtils.isNotEmpty(str)) {
                    result.add(str);
                }
            }
            br.close();
            reader.close();
        } catch (FileNotFoundException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        }
        return result;
    }

    /**
     * 读文件结果保存为一个字符串中
     */
    public static String readFileToString (String path) {
        File file02 = new File(path);
        FileInputStream is = null;
        StringBuilder stringBuilder = null;
        try {
            if (file02.length() != 0) {
                /**
                 * 文件有内容才去读文件
                 */
                is = new FileInputStream(file02);
                InputStreamReader streamReader = new InputStreamReader(is);
                BufferedReader reader = new BufferedReader(streamReader);
                String line;
                stringBuilder = new StringBuilder();
                while ((line = reader.readLine()) != null) {
                    // stringBuilder.append(line);
                    stringBuilder.append(line);
                }
                reader.close();
                is.close();
            } else {
                return "";
            }

        } catch (Exception e) {
            e.printStackTrace();
        }
        return String.valueOf(stringBuilder);

    }
    /**
     * 写入文件
     * @param path
     * @param
     */
    public static void writeToFile(String path ,String content) {
        FileWriter fw = null;
        try {
            //如果文件存在，则追加内容；如果文件不存在，则创建文件
            File f=new File(path);
            fw = new FileWriter(f, true);
        } catch (IOException e) {
            e.printStackTrace();
        }
        PrintWriter pw = new PrintWriter(fw);
        pw.println(content);
        pw.flush();
        try {
            fw.flush();
            pw.close();
            fw.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

    public static void deleteFile(String path) {
        File f = new File(path);
        if (f.exists()){
            f.delete();
        }
    }
}

```