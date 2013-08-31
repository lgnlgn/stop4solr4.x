stop4solr4.x
============

可以动态改变的停用词、同义词工厂类
在schema中添加
   <fieldType name="text_my" class="solr.TextField" positionIncrementGap="100">
     <analyzer type="index">
       <tokenizer class="solr.PatternTokenizerFactory" pattern="\s*?,\s*?"/>
     </analyzer>
	 <analyzer type="query">
       <tokenizer class="solr.PatternTokenizerFactory" pattern="\s*?,\s*?"/>
	   <filter class="org.apache.solr.analysis.DStopFilterFactory" conf="stop.conf" ignoreCase="true" enablePositionIncrements="true"/>
	   <filter class="org.apache.solr.analysis.DSynonymFilterFactory" conf="synonym.conf" ignoreCase="true" expand="true"/>
     </analyzer>
   </fieldType>
   
其中conf="xxxx"是配置词路径的，使用Properties的格式：
  lastupdate=11122
  files=stopwords.txt
  
lastupdate用来标明最后更新的时间，只要比上一次的大就会触发重新加载词库。files是需要读进来的文件路径，以英文逗号隔开
