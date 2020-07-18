# YouTubeExercise

QA Automation Engineer Exercise:
Automate the following scenario by using java and selenium. You can assume the information
or tools not mentioned and please mention the assumption you have made in a readme file.
Steps:
- Go to youtube.com
- Search for “selenium”
- Go to filter
- Sort by “upload date”
- Add the 3rd video in the search results to the queue using “Add to Queue” button
- Verify that this video is successfully added to the queue

Answer:- 

To Automate above Scenario I will be using Selenium Webdriver which is an open source tool to automate web browsers. It can
support many languages such as Java, C#, Python etc and it can support different operating systems and browsers.
Programming Language I will be using is Java as Selenium is more compatible with Java, because we will find a lot of
libraries which we can use to perform automation. First I will set the property for Chrome Driver, specify its location via the (webdriver.chrome.driver), then I will instantiate an instance of Chrome Driver which will be driving our browser after that I will navigate to YouTube. Once Navigate to YoutTube, I will click on Inspect icon to locate elements. 

public class YoutubeExercise {

public static void main(String[] args) throws InterruptedException {

System.setProperty("webdriver.chrome.driver","src/drivers/chromedriver");
WebDriver driver = new ChromeDriver();
driver.get("https://www.youtube.com/");
driver.manage().window().maximize();

driver.findElement(By.xpath("//input[@id='search']")).sendKeys("selenium");

driver.findElement(By.xpath("//button[@id='search-icon-legacy']")).click();
Thread.sleep(2000);

driver.findElement(By.xpath("//yt-icon[@class='style-scope ytd-toggle-button-renderer']")).click();

WebDriverWait wait = new WebDriverWait(driver, 10);
wait.until(ExpectedConditions.visibilityOfElementLocated(By.xpath("//div[@title='Sortby upload date']")));

driver.findElement(By.xpath("//div[@title='Sort by uploaddate']")).click();
Thread.sleep(2000);

WebElement video = driver.findElement(By.xpath("(//a[@id='video-title'])[3]"));

Actions ac = new Actions(driver);
ac.moveToElement(video).build().perform();

WebElement icon = driver.findElement(By.xpath("(//a[@id='video-title']//following::yt-icon[@class='style-scope ytd-menu-renderer'])[3]"));
icon.click();

driver.findElement(By.xpath("//yt-formatted-string[text()='Add toqueue']")).click();
Thread.sleep(2000);

WebElement queue =driver.findElement(By.xpath("//div[@class='channel style-scope ytd-miniplayer']"));

if (queue.isDisplayed()) {
System.out.println("It is successfully added to Queue!");
} else {
System.out.println("It is not successfully added to
Queue!");
}

driver.quit();
}
}
