---
title: java保留两位小数4种方法   
author: wuche  
layout: post  
permalink:  /java-map/  
tags:  
  - java  
    
  ---    
  java保留两位小数4种方法 


  ```java 
  public class format {
	      double f = 111231.5585;
	          public void m1() {
			          BigDecimal bg = new BigDecimal(f);
				          double f1 = bg.setScale(2, BigDecimal.ROUND_HALF_UP).doubleValue();
					          System.out.println(f1);
						      }
		      /**
			     * DecimalFormat转换最简便
			          */
		      public void m2() {
			              DecimalFormat df = new DecimalFormat("#.00");
				              System.out.println(df.format(f));
					          }
		          /**
			         * String.format打印最简便
				      */
		          public void m3() {
				          System.out.println(String.format("%.2f", f));
					      }
			      public void m4() {
				              NumberFormat nf = NumberFormat.getNumberInstance();
					              nf.setMaximumFractionDigits(2);
						              System.out.println(nf.format(f));
							          }
			      ```
