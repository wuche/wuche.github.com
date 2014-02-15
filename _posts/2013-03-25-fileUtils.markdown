---
layout: post
title: "fileUtils example"
description: "search for files use fileUitls"
tags: [development]
published: true
---
This example demonstrate how we can use the FileUtils class listFiles() method to search for a file specified by    
their extensions.


package info.perftest.wuche;

import org.apache.commons.io.FileUtils;

import java.io.File;
import java.util.Collection;
import java.util.Iterator;

public class SearchFiles {
    public static void main(String[] args) {
        File root = new File("/home/wuche/Personal/Examples");

        try {
            String[] extensions = {"xml", "java"};
            boolean recursive = true;

            //
            // Finds files within a root directory and optionally its
            // subdirectories which match an array of extensions. When the
            // extensions is null all files will be returned.
            //
            // This method will returns matched file as java.io.File
            //
            Collection files = FileUtils.listFiles(root, extensions, recursive);

            for (Iterator iterator = files.iterator(); iterator.hasNext();) {
                File file = (File) iterator.next();
                System.out.println("File = " + file.getAbsolutePath());
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}

