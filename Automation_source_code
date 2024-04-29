using NUnit.Framework;
using OpenQA.Selenium;
using OpenQA.Selenium.Chrome;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text.RegularExpressions;

namespace WikipediaUITest
{
    class Program
    {
        static void Main(string[] args)
        {
            // Create an instance of the WikipediaTest class
            var wikipediaTest = new WikipediaTest();

            // Call the Setup method to initialize the driver
            wikipediaTest.Setup();

            // Call the TestAutomationPageUITest method
            wikipediaTest.TestAutomationPageUITest();

            // Call the TearDown method to quit the driver
            wikipediaTest.TearDown();
        }
    }

    [TestFixture]
    public class WikipediaTest
    {
        private IWebDriver driver;
        private const string WikipediaUrl = "https://en.wikipedia.org/wiki/Test_automation";
        private const string TestDrivenDevelopmentSectionId = "Test-driven_development";

        [SetUp]
        public void Setup()
        {
            driver = new ChromeDriver();
            driver.Manage().Window.Maximize();
        }

        [TearDown]
        public void TearDown()
        {
            driver.Quit();
        }

        [Test]
        public void TestAutomationPageUITest()
        {
            // Step 1: Launch browser and navigate to Wikipedia page
            driver.Navigate().GoToUrl(WikipediaUrl);

            // Step 2: Extract text content from the Test-driven development section
            var testDrivenDevelopmentSectionText = GetSectionText(TestDrivenDevelopmentSectionId);

            // Step 3: Identify all unique words in the text
            var uniqueWords = GetUniqueWords(testDrivenDevelopmentSectionText);

            // Step 4: Print the number of occurrences for each word
            PrintWordOccurrences(uniqueWords);
        }

        private string GetSectionText(string sectionId)
        {
            var sectionElement = driver.FindElement(By.Id(sectionId));
            return sectionElement.Text;
        }

        private IEnumerable<string> GetUniqueWords(string text)
        {
            // Step 4: Exclude brackets and their contents
            text = Regex.Replace(text, @"\[.*?\]", "");

            // Step 5: Disregard periods, hyphens, commas, and other delimiters from any word
            text = Regex.Replace(text, @"[^\w\s]", "");

            // Step 6: Transform to lowercase and split into words
            var words = text.ToLower().Split(new[] { ' ' }, StringSplitOptions.RemoveEmptyEntries);

            // Step 7: Identify unique words
            var uniqueWords = new HashSet<string>(words);
            return uniqueWords;
        }

        private void PrintWordOccurrences(IEnumerable<string> words)
        {
            var wordCount = new Dictionary<string, int>();

            foreach (var word in words)
            {
                if (wordCount.ContainsKey(word))
                {
                    wordCount[word]++;
                }
                else
                {
                    wordCount[word] = 1;
                }
            }

            Console.WriteLine("***********output for automation testing*************");
            foreach (var kvp in wordCount)
            {
                Console.WriteLine($"{kvp.Key}: {kvp.Value}");
            }
        }
    }
}
