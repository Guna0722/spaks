vfrom selenium import webdriver
import time
from selenium.webdriver.chrome.options import Options
from selenium.webdriver.common.keys import Keys
from selenium.common.exceptions import NoSuchElementException
from selenium.webdriver.support.ui import Select
from selenium.webdriver import ActionChains
from webdriver_manager.chrome import ChromeDriverManager

opt = Options()
opt.add_argument("start-maximized")
opt.add_argument("--disable-extensions")
opt.add_experimental_option("prefs", { \
"profile.default_content_setting_values.media_stream_mic": 1,
"profile.default_content_setting_values.media_stream_camera": 1,
"profile.default_content_setting_values.geolocation": 1,
"profile.default_content_setting_values.notifications": 1
})

wdriver = webdriver.Chrome(ChromeDriverManager().install())
wdriver.maximize_window()
wdriver.get("https://www.thesparksfoundationsingapore.org/")


# Test 1:check Title
print("\nTestCase 1:")
if wdriver.title:
    print("\nTitle Verified Successfully: ", wdriver.title)
else:
    print("\nTitle Verification Failed!\n")

# Test 2: check logo
print("\nTestCase 2:")
try:
    wdriver.find_element_by_xpath('//*[@id="home"]/div/div[1]/h1/a/*').click()
    print('Success! The logo is present\n')
    time.sleep(3)
except NoSuchElementException:
    print('No logo is present!\n')

# Test 3: Check for navbar 
print("TestCase 3:")
try:
    wdriver.find_element_by_class_name("navbar")
    print("Navbar Verification Successful!\n")
except NoSuchElementException:
    print("Navbar Verification Failed!\n")

# Test 4:check for Home button
print("TestCase 4:")
try:
    wdriver.find_element_by_partial_link_text("The Sparks Foundation").click()
    print("Home link is working!\n")
except NoSuchElementException:
    print("Home Link Doesn't Work!\n")


# Test 5:check for About Us Page
print("TestCase 5:")
try:
    wdriver.find_element_by_link_text('About Us').click()
    time.sleep(3)
    wdriver.find_element_by_link_text('Corporate Partners').click()
    time.sleep(3)
