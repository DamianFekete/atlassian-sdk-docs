---
aliases:
- /server/framework/atlassian-sdk/getting-custom-fields-from-confluence-v2-searches-2818390.html
- /server/framework/atlassian-sdk/getting-custom-fields-from-confluence-v2-searches-2818390.md
category: devguide
confluence_id: 2818390
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818390
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818390
platform: server
product: atlassian-sdk
subcategory: faq
title: Getting Custom Fields From Confluence V2 Searches 2818390
---
# Getting custom fields from Confluence V2 Searches

If you use an [extractor module](https://developer.atlassian.com/display/CONFDEV/Extractor+Module) in your Confluence plugin to add additional information to the Lucene search index there is currently no way to access these fields using the [V2 Search API](https://developer.atlassian.com/display/CONFDEV/Searching+Using+the+V2+Search+API). You can use these fields in custom search queries or sorts, but actually reading these fields from the returned data is not possible with the current API.

## Limitations of the Current API

When you do a search using the V2 Search API the <a href="http://docs.atlassian.com/atlassian-confluence/latest/com/atlassian/confluence/search/v2/SearchManager.html" class="external-link">SearchManager.search(..)</a> method Confluence will give you back a <a href="http://docs.atlassian.com/atlassian-confluence/latest/com/atlassian/confluence/search/v2/SearchResults.html" class="external-link">SearchResults</a> object. You can then retrieve each of the individual <a href="http://docs.atlassian.com/atlassian-confluence/latest/com/atlassian/confluence/search/v2/SearchResult.html" class="external-link">SearchResult</a> objects that matched your search.

The `SearchResult` interface contains a <a href="http://docs.atlassian.com/atlassian-confluence/latest/com/atlassian/confluence/search/v2/SearchResult.html#getExtraFields%28%29" class="external-link">getExtraFields()</a> method which is supposed to return additional fields that cannot be directly accessed by this interface. Unfortunately the <a href="http://docs.atlassian.com/atlassian-confluence/latest/com/atlassian/confluence/search/v2/lucene/LuceneSearchResults.html" class="external-link">LuceneSearchResult</a> implementation has hardcoded the fields that are returned. This means that if you have an extractor module that has added custom fields to the index they can not be retrieved using the SearchResult interface.

## Wrapping the SearchResult Object with custom implementation

If you look at the source code for the LuceneSearchResult class, you will see that all of the index document fields are stored in a private map called *results*. You can use java reflection to get access to this field within your own plugin classes.

The following example wraps the `LuceneSearchResult` providing access to the internal results field.

``` java
public class LuceneV2Result {

    static private Field resultsField;

    static {
        try {
            resultsField = LuceneSearchResult.class.getDeclaredField("results");
            resultsField.setAccessible(true);
        } catch (Exception e) {
            // :(
        }
    }

    Map<String, String> fields;
   

    @SuppressWarnings("unchecked")
    public LuceneV2Result(SearchResult result) {
        try {
            fields = (Map) resultsField.get(result);
        } catch (Exception e) {
            // :(
        }
    }
    
    public Map<String, String> getFields(){
        return fields;
    }   
}
```

{{% note %}}

It should be noted that this implementation is highly likely to break in future releases if Atlassian change the internal implementation of this class. Hopefully by that time there will be a way to access custom extractor fields directly.

{{% /note %}}






































































































