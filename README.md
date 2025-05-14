import com.microsoft.playwright.*;
import java.nio.file.Paths;

public class MobilePageBody {
  public static void main(String[] args) {
    try (Playwright playwright = Playwright.create()) {
      Browser browser = playwright.chromium().launch(new BrowserType.LaunchOptions().setHeadless(false));

      Browser.NewContextOptions options = new Browser.NewContextOptions()
          .setViewportSize(390, 844)
          .setUserAgent("Mozilla/5.0 (iPhone; CPU iPhone OS 14_0 like Mac OS X) AppleWebKit/...");

      BrowserContext context = browser.newContext(options);
      Page page = context.newPage();

      Response response = page.navigate("https://example.com");

      if (response != null) {
        String body = response.text();
        System.out.println("Page Response Body:");
        System.out.println(body);
      } else {
        System.out.println("No response received.");
      }

      browser.close();
    }
  }
}
