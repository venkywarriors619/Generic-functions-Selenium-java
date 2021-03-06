## Commonly used functions in Selenium webdriver
### :dart:Check Element Exists: <br> 
```	
	public static  void waitForElement(WebDriver driver, String locator) 
	{				
			 String[] arrOfStr = locator.split("#"); 

		if (arrOfStr[0].equalsIgnoreCase("xpath"))
		{
			if(driver.findElements(By.xpath(arrOfStr[1])).size() != 0){
				return true;
			}
		}       
		if (arrOfStr[0].equalsIgnoreCase("id"))
		{
			if(driver.findElements(By.id(arrOfStr[1])).size() != 0){
				return true;
			}
		}
		if (arrOfStr[0].equalsIgnoreCase("name"))
		{
			if(driver.findElements(By.name(arrOfStr[1])).size() != 0){
				return true;
			}
		}
		if (arrOfStr[0].equalsIgnoreCase("link"))
		{
			if(driver.findElements(By.linkText(arrOfStr[1])).size() != 0){
				return true;
			}
		}
			return false;

	}
```
### :dart:How to switch to another Tab using Selenium WebDriver with Java
```
public boolean switchToTab(String tabName){
    //count no of tab
    ArrayList<String> tab = new ArrayList<>(driver.getWindowHandles());
    System.out.println("No. of tabs: " + tabs.size());
    ArrayList<String> tabList = new ArrayList<>();
    for (int i =0;i<tab.size();i++){
        tabList.add(i,driver.switchTo().window(tab.get(i)).getTitle());
        driver.switchTo().window(tab.get(0));
        if(tabList.get(i).equals(tabName)){
            driver.switchTo().window(tab.get(i));
                return true;
        }
    }
    return false;
}
```
```
Robot r = new Robot();
        r.keyPress(KeyEvent.VK_CONTROL);
        r.keyPress(KeyEvent.VK_T);
        r.keyRelease(KeyEvent.VK_CONTROL);
        r.keyRelease(KeyEvent.VK_T);
        Thread.sleep(1000);
```
### :dart:WebDriver Wait For Page to Load: <br> 
```	
	public void waitForPageLoaded(WebDriver driver) {
		ExpectedCondition<Boolean> expectation = new
			ExpectedCondition<Boolean>() {
			    public Boolean apply(WebDriver driver) {
				return ((JavascriptExecutor) driver).executeScript("return document.readyState").toString().equals("complete");
			    }
			};
		try {
		    Thread.sleep(1000);
		    WebDriverWait wait = new WebDriverWait(driver, 30);
		    wait.until(expectation);
		} catch (Throwable error) {
		    Assert.fail("Timeout waiting for Page Load Request to complete.");
		}
	    }
    
```
```
public void waitForLoad(WebDriver driver) {
        ExpectedCondition<Boolean> pageLoadCondition = new
                ExpectedCondition<Boolean>() {
                    public Boolean apply(WebDriver driver) {
                        return ((JavascriptExecutor)driver).executeScript("return document.readyState").equals("complete");
                    }
                };
        WebDriverWait wait = new WebDriverWait(driver, 30);
        wait.until(pageLoadCondition);
    }
```
### :dart:Get current timestamp: <br> 
```	
	public static String timestamp() 
		{
				
		Calendar calaender = Calendar.getInstance();
		String timestp = new SimpleDateFormat("dd_MM_yyyy_hh_mm_ss").format(calaender.getTime());
		return timestp;
		
		}
```
### :dart:Select value from dropdown by Visibliblty of Text: <br> 
```	
	public static void selctvalue(WebElement element, String value) 
	{
			
		Select drpvalue = new Select(element);
		drpvalue.selectByVisibleText(value);
	
	}
```
### :dart:Clear text in edit box and enter text <br> 
```
public static void clearAndEnterText(WebElement element, String value) 
	{
		element.sendKeys(Keys.chord(Keys.CONTROL,"a", Keys.DELETE));
		element.sendKeys(value);
	}
```
### :dart:Create Folder: <br> 
```	
	public static String checkFolderandCreateFolder(String folderpath) 
	{
			
		File createDir = new File (folderpath);
		if (!createDir.exists())
		{
			createDir.mkdir();
		}
		else
		{
			System.out.println("Folder creted "+folderpath.toString());
		}	
		return createDir.getAbsolutePath().toString();
	
	}
```
### :dart:Check for element exists: <br> 
```	
	public static boolean isElementdisplayed(WebDriver driver, String Xpath) 
	{
		
		if(driver.findElements(By.xpath(Xpath)).size() != 0){
			return true;
			}else{
				return false;
			}				
	}
```
### :dart:Get system Host Name: <br> 
```	
	public static String getHostName()
	{
			
		InetAddress localhost = null;
		try {
			localhost = InetAddress.getLocalHost();
		} catch (UnknownHostException e) {
			
			e.printStackTrace();
		}
	
		return localhost.getHostName().toString();
	
	}
```
### :dart:Scroll and Highlight Webelement: <br> 
```		
	public static void scrollandhighlight(WebDriver driver, WebElement element) throws InterruptedException {
		JavascriptExecutor js = (JavascriptExecutor) driver;
		js.executeScript("arguments[0].scrollIntoView(true);", element);
		js.executeScript("arguments[0].style.border='4px solid red'", element);
		Thread.sleep(2000);
		js.executeScript("arguments[0].style.border=''", element);
	}
```
#### Highlight Webelement: <br> 
```	
	public static void highlightElement(WebDriver driver, WebElement element) throws InterruptedException {
		JavascriptExecutor js = (JavascriptExecutor) driver;
		js.executeScript("arguments[0].style.border='4px solid yellow'", element);
		Thread.sleep(2000);
		js.executeScript("arguments[0].style.border=''", element);
	}
```
### :dart:Capture ScreenShot: <br> 
```	
	public static String captureScreen(WebDriver driver, String screenshotPath, String fileName, String status) {
		if (fileName == "") {
			fileName = "blank";
		}
		File destFile = null;
		File scrFile = ((TakesScreenshot) driver).getScreenshotAs(OutputType.FILE);

		try {
			
			destFile = new File((String) screenshotPath +"/" + fileName + "_" + status + ".png");
			FileUtils.copyFile(scrFile, destFile);
		} catch (IOException e) {
			e.printStackTrace();
		}
		return destFile.getAbsolutePath().toString();
	}

```
#### Capture Screenshot Using Robot Class: <br> 
```	
	public static String captureScreen(String screenshotPath, String fileName) {
		if (fileName == "") {
			fileName = "blank";
		}
		Robot r=new Robot();
 		Dimension screensize = Toolkit.getDefaultToolkit().getScreenSize();
 		Rectangle screenRect=new Rectangle(screensize);
 		BufferedImage image=r.createScreenCapture(screenRect);
		try {
			
			destFile = new File((String) screenshotPath +"/" + fileName + ".png");
			 ImageIO.write(image, "png",new File(destFile));
		} catch (IOException e) {
			e.printStackTrace();
		}
		return destFile.getAbsolutePath().toString();
	}

```
#### Capture full Page ScreenShot using AShot : <br> 
```	
	public static String fullPageScreenshot (WebDriver driver, String screenshotPath, String fileName, String status) {
		if (fileName == "") {
			fileName = "blank";
		}
		String destFile = null;
				
		try {
			
			destFile = screenshotPath +"/" + fileName + "_" + status + ".png";
			Screenshot fpScreenshot = new  	AShot().shootingStrategy(ShootingStrategies.viewportPasting(1000)).takeScreenshot(driver);
		     ImageIO.write(fpScreenshot.getImage(),"PNG",new File(destFile));

		} catch (IOException e) {
			e.printStackTrace();
		}
		return destFile;
	}
```
#### How to Capture WebElement Screenshot
```
WebElement element = driver.findElement(By.id("imagetrgt"));
         
        File source = ((TakesScreenshot)element).getScreenshotAs(OutputType.FILE);
        FileHandler.copy(source, new File("./screenshots/element.png"));
        Thread.sleep(3000);
```
Element screenshot by cropping entire page 
```
driver.get("http://www.google.com");
WebElement ele = driver.findElement(By.id("hplogo"));

// Get entire page screenshot
File screenshot = ((TakesScreenshot)driver).getScreenshotAs(OutputType.FILE);
BufferedImage  fullImg = ImageIO.read(screenshot);

// Get the location of element on the page
Point point = ele.getLocation();

// Get width and height of the element
int eleWidth = ele.getSize().getWidth();
int eleHeight = ele.getSize().getHeight();

// Crop the entire page screenshot to get only element screenshot
BufferedImage eleScreenshot= fullImg.getSubimage(point.getX(), point.getY(),
    eleWidth, eleHeight);
ImageIO.write(eleScreenshot, "png", screenshot);

// Copy the element screenshot to disk
File screenshotLocation = new File("C:\\images\\GoogleLogo_screenshot.png");
FileUtils.copyFile(screenshot, screenshotLocation);
```
### :dart:Press Tab Key Using Action Class : <br> 
```
	public boolean pressTabKey(Webdriver driver)
 	{
 		Actions act=new Actions(driver);
		act.sendKeys(Keys.TAB).build().perform();
 	}

```
### :dart:Double Click Using Action Class : <br> 
```
	public boolean doubleClick(Webdriver driver)
 	{
 		Actions act=new Actions(driver);
		act.moveToElement(Element).build().perform();
 		Thread.sleep(5000);
 		act.click().build().perform()
 	}
```
### :dart:Drag Drop Using Action Class : <br> 
```
	public boolean dragAndDrop(Webdriver driver,WebElement source,WebElement destination)
 	{
 		Actions act=new Actions(driver);
		act.dragAndDrop(source, destination).build().perform();
 	}

```
### :dart:Open New Tab Using Selenium WebDriver 
```
	 public void openNewTab(WebDriver driver) throws InterruptedException
	 {
		ArrayList<String> tabs = new ArrayList<String>(driver.getWindowHandles());
		driver.switchTo().window(tabs.get(0));
		Thread.sleep(5000);
   	 }
```
### :dart:Get Browser Name Using JavascriptExecutor : <br> 
```
	public String browserName(Webdriver driver)
 	{
 		JavascriptExecutor js = (JavascriptExecutor) driver;
 		String browsername=js.executeScript("return navigator.appCodeName");
		return browsername;
 	}

```
### :dart:Check if element is disable using selenium : <br> 
```
	public boolean checkEnabled(WebElement element)
 	{
 		if (element.isEnabled())
		{
			return element.isEnabled();
		}
		else
		{	
			return false;
 		}
```
### :dart:Capture Tooltip in Selenium : <br> 
```
	public String getTooltip(Webdriver driver, WebElement tooltip) 
	{
		Actions builder=new Actions(driver);
		builder.moveToElement(tooltip).perform();
		String tooltip_msg=tooltip.getAttribute("title");
		return tooltip_msg;
	}
```
### :dart:Bootstrap drop down handling in selenium : <br> 
```

	public boolean bootstrapdropdown(WebElement bootstrap, String dropdownValue) 
	{
		// elements and findElements will return list of WebElements

		List<WebElement> list = bootstrap;
		int counter=0;

		for (WebElement ele : list) 
		{ 
			if (ele.getAttribute("innerHTML").contains(dropdownValue)) {
			     ele.click();
			     counter=counter+1;
			     break;
			  }
		 }

		if (counter != 0)    { return true; }
		else { return false; }
	}
```
### :dart:Browser Utility function: <br> 
```
public static  WebDriver browserUtility(String browser, String URL) 
	{
				
		 if(browser.equalsIgnoreCase("chrome")) {			 
			   System.out.println("*** launching chrome browser ***");
			   System.setProperty("webdriver.chrome.driver", System.getProperty("user.dir")+"/driver/chromedriver.exe");
			   driver=new ChromeDriver();  			 
		 }else if (browser.equalsIgnoreCase("ie")) { 			 
				  System.out.println("*** launching IE browser ***");
				  System.setProperty("webdriver.ie.driver", System.getProperty("user.dir")+"/driver/IEDriverServer.exe");
				  driver = new InternetExplorerDriver();
		 }else if (browser.equalsIgnoreCase("edge")) { 			 
					  System.out.println("*** launching Microsoft Edge browser ***");
					  System.setProperty("webdriver.edge.driver", System.getProperty("user.dir")+"/driver/MicrosoftWebDriver.exe"); 
					  driver = new EdgeDriver();
		 }else if (browser.equalsIgnoreCase("Firefox")) { 			 
			  System.out.println("*** launching Firefox browser ***");
			  System.setProperty("webdriver.edge.driver", System.getProperty("user.dir")+"/driver/geckodriver.exe"); 
			  driver = new EdgeDriver();
		 }else if (browser.equalsIgnoreCase("headless browser")) { 			 
			  driver = new HtmlUnitDriver(); 
		 } 		
		 driver.navigate().to(URL);
		  driver.manage().deleteAllCookies();
		 driver.manage().window().maximize();
		 driver.manage().timeouts().pageLoadTimeout(property.getpageTimeOut(), TimeUnit.SECONDS);
		 return driver;
	}
```

