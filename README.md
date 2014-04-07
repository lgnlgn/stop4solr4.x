stop4solr4.x（不再维护，未来可能删除：请去https://github.com/mlcsdev/mlcsseg）
============

可以动态改变的停用词、同义词工厂类，**只支持solr4.4**，（如果你是4.4以下的，在POM中引入旧的solr再修改以下源码）

DStopFilterFactory

DSynonymFilterFactory


在schema中添加

```xml
<fieldType name="text_my" class="solr.TextField" positionIncrementGap="100">

  <analyzer type="index">
    <tokenizer class="solr.PatternTokenizerFactory" pattern="\s*?,\s*?"/>
  </analyzer>

  <analyzer type="query">
    <tokenizer class="solr.PatternTokenizerFactory" pattern="\s*?,\s*?"/>
    <filter class="org.apache.solr.analysis.DStopFilterFactory" conf="stop.conf" ignoreCase="true"
            enablePositionIncrements="true"/>
    <filter class="org.apache.solr.analysis.DSynonymFilterFactory" conf="synonym.conf" ignoreCase="true" expand="true"/>
  </analyzer>

</fieldType> 
```

其中conf="xxxx"是配置词路径的，使用Properties的格式：

  lastupdate=11122

  files=stopwords.txt
  
lastupdate用来标明最后更新的时间，只要比上一次的大就会触发重新加载词库。files是需要读进来的文件路径，以英文逗号隔开
