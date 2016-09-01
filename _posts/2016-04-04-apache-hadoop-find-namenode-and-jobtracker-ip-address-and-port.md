---
title: "Apache Hadoop: Find nameNode and jobTracker IP address and port"
description: ""
category: hadoop
tags: [oozie, namenode,jobtracker]
sidebar:
  nav: "new_side"
---


Before being compared two files they must be aligned, the alignment rule can be configured

# Align by Name Case Sensitivity

The default alignment method compares file name strings, if they are match case then they will be aligned.  
Suppose you have the scenario shown below

<div class="table-wrapper">
    <table class="alt">
        <thead>
            <tr>
                <th>Left</th>
                <th>Right</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td>winter.jpg</td>
                <td>&nbsp;</td>
            </tr>
            <tr>
                <td>&nbsp;</td>
                <td>WINTER.JPG</td>
            </tr>
            <tr>
                <td>summer.jpg</td>
                <td>summer.jpg</td>
            </tr>
        </tbody>
    </table>
</div>

By default winter.jpg and WINTER.JPG will be not aligned because their strings don't match uppercase and lowercase characters.  
This result sometimes isn't what you expect, maybe you want to ignore uppercase/lowercase differences.  
This can be achieved selecting 'Ignore File Name Case' from popup menu.</p>
