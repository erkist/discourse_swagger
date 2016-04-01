# discourse_swagger
Provides a Swagger specification of the Discourse REST API, that can be used to generate Discourse API clients
## Examples

### Java
```java
    ApiClient client = new ApiClient();
    client.setBasePath("http://192.168.56.2");

    DefaultApi api = new DefaultApi(client);

    ((ApiKeyAuth) client.getAuthentication("api_username")).setApiKey("erki");
    ((ApiKeyAuth) client.getAuthentication("api_key"))
        .setApiKey("35b1416dda787a137dddca95170a549e0445507fcabcd009c09d3569cdb527b7");

    //Get site information
    Site site = api.getSite();
    String nameOfFirstTopMenuItem = site.getTopMenuItems().get(0);
    System.out.println(nameOfFirstTopMenuItem);

    //Get information about available categories
    CategoriesResponse categoriesResponse = api.getCategories();
    String slugOfThirdCategory = categoriesResponse.getCategoryList().getCategories().get(3).getSlug();
    System.out.println("First category slug: " + slugOfThirdCategory);
    
    //Get a single category
    CategoryResponse categoryResponse = api.getCategory(slugOfThirdCategory);
    String slugOfFirstTopic = categoryResponse.getTopicList().getTopics().get(0).getSlug();
    System.out.println("First topic slug: " + slugOfFirstTopic);
    
    //Get single topic
    TopicView topicView = api.getTopic(slugOfFirstTopic);
    String contentOfFirstPost = topicView.getPostStream().getPosts().get(0).getCooked();
    
    System.out.println(contentOfFirstPost.substring(0, Math.min(100, contentOfFirstPost.length())));
```
