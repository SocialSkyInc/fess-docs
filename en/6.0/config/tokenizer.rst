========================================
Settings for the index string extraction
========================================

This page is generated by Machine Translation from Japanese.

About the index string extraction
=================================

You must isolate the document in order to register as the index when
creating indexes for the search. Tokenizer is used for this.

Basically, carved by the tokenizer units smaller than go find no hits.
For example, statements of living in Tokyo, Japan. Was split by the
tokenizer now, this statement is in Tokyo, living and so on. In this
case, in Tokyo, Word search, you will get hit. However, when performing
a search with the word 'Kyoto' will not be hit. For selection of the
tokenizer is important.

You can change the tokenizer by setting the schema.xml analyzer part is
if the |Fess| in the default CJKTokenizer used.

About CJKTokenizer
------------------

Such as CJKTokenizer Japan Japanese multibyte string against bi-gram, in
other words two characters create index. In this case, can't find one
letter words.

About StandardTokenizer
-----------------------

StandardTokenizer creates index uni-gram, in other words one by one for
the Japan language of multibyte-character strings. Therefore, the less
search leakage. Also, with StandardTokenizer can't CJKTokenizer the
search query letter to search to. However, please note that the index
size increases.

The following example to change the analyzer part like
solr/core1/conf/schema.xml, you can use the StandardTokenizer.

::

    <schema name="fess" version="1.4">
      <types>
        <fieldType name="text" class="solr.TextField" positionIncrementGap="100">
          <analyzer type="index">
            <charFilter class="solr.MappingCharFilterFactory" mapping="mapping_ja.txt"/>
            <tokenizer class="solr.StandardTokenizerFactory"/>
      :
          </analyzer>
          <analyzer type="query">
            <charFilter class="solr.MappingCharFilterFactory" mapping="mapping_ja.txt"/>
            <tokenizer class="solr.StandardTokenizerFactory"/>
      :

Also, useBigram is enabled by default in the
webapps/fess/WEB-INF/classes/app.dicon change to false.

::

      :
        <component name="queryHelper" class="jp.sf.fess.helper.impl.QueryHelperImpl">
            <property name="useBigram">true</property>
      :

After the restart the |Fess| .
