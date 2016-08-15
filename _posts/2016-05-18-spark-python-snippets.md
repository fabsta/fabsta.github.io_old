---
title: "Spark python snippets"
description: ""
category: snippets 
tags: [snippets]
---

<link href="assets/css/syntax.css" rel="stylesheet">


### Table of contents

* TOC
{:toc}



## Spark code snippets


<p>
    Paragraph code example<br>
    that needs multiple lines
</p>


{% highlight python linenos %}
def show
  puts "Outputting a very lo-o-o-o-o-o-o-o-o-o-o-o-o-o-o-o-ong lo-o-o-o-o-o-o-o-o-o-o-o-o-o-o-o-ong line"
  @widget = Widget(params[:id])
  respond_to do |format|
    format.html # show.html.erb
    format.json { render json: @widget }
  end
end
{% endhighlight %}



###Clean bad data
{% highlight python linenos %}
%pyspark
from pyspark.sql import SQLContext
sqlContext = SQLContext(sc)
from extension_utils import ExtensionUtils
eu = ExtensionUtils(sqlContext)


df = sqlContext.read.format("com.ibm.spark.discover").load("/resources/data/sparklingdata/data/sampleDataDir/")
df.printSchema()

{% endhighlight %}




### showing data

// prints table 

dataframe.show()

// z = context
z.show(dataframe)


### merging data

{% highlight python linenos %}

var ap_all_df = ap_co_df
	.unionAll(ap_so2_df)
	.unionAll(ap_no2_df)
	.unionAll(ap_o3_df)

{% endhighlight %}




### grouping data

{% highlight python linenos %}


var sum_df = ap_all_df
	.groupBy($"Parameter Name")
	.agg(Map("Sample Measurement" -> "sum"))

{% endhighlight %}


### Dataframe

#### filter (equal to)

val noheader_df = dailyCA_filtered_df.filter(!dailyCA_df("C6").equalTo("TMAX")).filter(!dailyCA_df("C3").equalTo("unknown"))


####  filer x > 3 
{% highlight python linenos %}
val nocal_df = noheader_df.filter("C3 > 38")

{% endhighlight %}
### Spark SQL

#### Casting

select C5 as DATE, cast(avg(C6)/10 as DOUBLE) as TMAX from nocal group by C5 order by DATE asc


{% highlight python linenos %}
select C5 as DATE, 
cast(avg(C6)/10 as DOUBLE) as TMAX, 
cast(avg(c11)/10 as DOUBLE) as TMIN
from dailyCAWeather
where C6 <> 'TMAX' group by C5 order by DATE asc
		 
{% endhighlight %}




### Data export

#### csv
{% highlight python linenos %}
allData
    .repartition(1)
    .write
    .format("com.databricks.spark.csv")
    .option("header", "true")
    .save("alldata.csv") 
{% endhighlight %}

