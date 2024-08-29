-<dependencies>
    <!-- Selenium Java Dependency -->
    <dependency>
        <groupId>org.seleniumhq.selenium</groupId>
        <artifactId>selenium-java</artifactId>
        <version>4.10.0</version>
    </dependency>

    <!-- WebDriver Manager Dependency for managing drivers -->
    <dependency>
        <groupId>io.github.bonigarcia</groupId>
        <artifactId>webdrivermanager</artifactId>
        <version>5.3.1</version>
    </dependency>
</dependencies>


import io.github.bonigarcia.wdm.WebDriverManager;
import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.chrome.ChromeDriver;

import java.time.LocalDate;
import java.time.format.DateTimeFormatter;

public class DinggBookingAutomation {

    public static void main(String[] args) {
        WebDriverManager.chromedriver().setup();
        WebDriver driver = new ChromeDriver();

        try {
            // Step 1: Login to the website
            driver.get("https://stg.dingg.app/");
            driver.findElement(By.id("email")).sendKeys("ui-automation@gmail.com");
            driver.findElement(By.id("password")).sendKeys("dingg@1234");
            driver.findElement(By.xpath("//button[text()='Login']")).click();

            // Wait for the page to load (you may want to add explicit waits here)
            Thread.sleep(3000);

            // Step 2: Book an appointment for TODAY
            driver.findElement(By.xpath("//a[text()='Book Appointment']")).click();
            driver.findElement(By.xpath("//input[@placeholder='Select Date']")).click();

            // Selecting today's date
            String today = LocalDate.now().format(DateTimeFormatter.ofPattern("yyyy-MM-dd"));
            driver.findElement(By.xpath("//td[@data-date='" + today + "']")).click();

            // Assume selecting staff and confirming booking (use appropriate locators as needed)
            driver.findElement(By.xpath("//select[@name='staff']")).click();
            driver.findElement(By.xpath("//option[text()='Staff Member 1']")).click();
            driver.findElement(By.xpath("//button[text()='Confirm']")).click();

            // Step 3: Mark Start and Complete Service
            Thread.sleep(3000);
            driver.findElement(By.xpath("//button[text()='Start Service']")).click();
            Thread.sleep(2000);
            driver.findElement(By.xpath("//button[text()='Complete Service']")).click();

            // Step 4: Generate Bill and Checkout
            Thread.sleep(2000);
            driver.findElement(By.xpath("//button[text()='Checkout']")).click();

            // Add a product to the bill
            driver.findElement(By.xpath("//button[text()='Add Product']")).click();
            driver.findElement(By.xpath("//input[@placeholder='Search Product']")).sendKeys("Product 1");
            driver.findElement(By.xpath("//button[text()='Add to Bill']")).click();

            // Finalize and complete the checkout
            driver.findElement(By.xpath("//button[text()='Generate Invoice']")).click();

        } catch (InterruptedException e) {
            e.printStackTrace();
        } finally {
            // Close the browser
            driver.quit();
        }
    }
}
