# fail to pass some gc related test #

from /java/org/apache/commons/beanutils/BeanificationTestCase.java
```
	/** Test of the methodology we'll use for some of the later tests */
    public void testMemoryTestMethodology() throws Exception {
        // test methodology
        // many thanks to Juozas Baliuka for suggesting this method
        ClassLoader loader = new ClassLoader(this.getClass().getClassLoader()) {};
        WeakReference reference = new  WeakReference(loader);
        Class myClass = loader.loadClass("org.apache.commons.beanutils.BetaBean");
        
        assertNotNull("Weak reference released early", reference.get());
        
        // dereference class loader and class:
        loader = null;
        myClass = null;
        
        int iterations = 0;
        int bytz = 2;
        while(true) {
            System.gc();
            if(iterations++ > MAX_GC_ITERATIONS){
                fail("Max iterations reached before resource released.");
            }
            if( reference.get() == null ) {
                break;
                
            } else {
                // create garbage:
                byte[] b =  new byte[bytz];
                bytz = bytz * 2;
            }
        }
    }
```
dex2jar translate to
```
  public void testMemoryTestMethodology()
    throws Exception
  {
    BeanificationTestCase.1 local1 = new BeanificationTestCase.1(this, getClass().getClassLoader());
    WeakReference localWeakReference = new WeakReference(local1);
    local1.loadClass("org.apache.commons.beanutils.BetaBean");
    assertNotNull("Weak reference released early", localWeakReference.get());
	
	// local1=null;  !not translated
	// localWeakReference=null; !not translated
	
    int i = 0;
    int j = 2;
    while (true)
    {
      System.gc();
      int k = i + 1;
      if (i > 50)
        fail("Max iterations reached before resource released.");
      if (localWeakReference.get() == null)
        return;
      new byte[j];
      j *= 2;
      i = k;
    }
  }
```
Reason: if same var be assigned twice or more dex2jar will treat them as different var, so if we use aaa=null; to release resource,
dex2jar will ignore the assignment. so the resource is not released during the method execution.

