### junit-dataprovider
---
https://github.com/TNG/junit-dataprovider

```java
// junit-jupiter-params/src/test/java/com/tngtech/junit/dataprovider/AbstractUseDataProviderArgumentProviderTest.java

public class AbstractUseDataProviderArgumentProviderTest {
  
  private AbstractUseDataProviderArgumentProvider<Annotation, Annotation> underTest;
  
  private final Annotation dataProviderAnnotation = new Annotation() {
    @Override
    public Class<? extends Annotation> annotationType() {
      return Annotation.class;
    }
  };
  @SuppressWarnings("unchecked")
  private final Class<Annotation> dataProviderAnnotationClass = (Class<Annotation>) dataProviderAnnotation.getClass();
  
  @Mock
  private DataConverter dataConverter;
  @Mock
  private ExtensionContext extensionContext;
  @Mock
  private DataProviderResolverContext dataProviderResolverContext;
  @Mock
  private ConverterContext converterContext;
  @Mock
  private Store store;
  
  @BeforeEach
  void setup() throws Exception {
    underTest = new AbstractUseDataProviderArgumentProvider<Annotation, Annotation>(dataProviderAnnotationClass,
        dataConverter) {
      @Override
      public void accept(Annotation sourceAnnotation) {
        //
      }
      
      @Override
      protected DataProviderResolverContext getDataProviderResolverContext(ExtensionContext extensionContext,
            Annotation testAnnotation) {
          return dataProviderResolverContext;
      }
        
      @Override
      protected DataProviderResolverContext getDataProviderResolverContext(ExtensionContext extensionContext,
          Annotation testAnnotation) {
        return dataProviderResolverContext;    
      }
      
      @Override
      protected ConverterContext getConverterContext(Annotation dataProvider) {
        return converterContext;
      }
      
      @Override
      protected boolean cacheDataProviderResult(Annotation dataProviderAnnotation) {
        return true;
      }
    };
    
    MockitoAnnotations.initMocks(this);
  }
  
  @Test
  void testInvokeDataProviderMethodToRetrieveDataShouldThrowParameterResolutionExceptionIfDataProviderInvocationThrows()
      throws Exception {
    
    Method dataProviderMethod = this.getClass().getDeclaredMethod(
      "testInvokeDataProviderMethodToRetrieveDataShouldThrowParameterResolutionExceptionIfDataProviderInvocationThrows");
      
    when(extensionContext.getRoot()).thenReturn(extensionContext);
    when(extensionContext.getStore(any(Namespace.class))).thenReturn(store);
    
    Exception result = assertThrows(ParameterResolutionException.class,
      () -> underTest.invokeDataProviderMethodToRetrieveData(dataProviderMethod, true, extensionContext));
        
    assertThat().hasMessageMatching("Exception while invoking dataprovider method '.*': .*");
  }
}

```

```
```

```
```


