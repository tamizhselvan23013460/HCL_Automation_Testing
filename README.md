# HCL_Automation_Testing

## 05-10-2026 : 

1. Project 1: Google Search – Open Actor Simbu Search Results 

2. Project 2: SauceDemo Login and Product Listing 

3. Project 3: OTP-Based Login Automation – Flipkart QA Approach 


## 06-10-26 : 

1. **How do you automate filling out the Vinoth QA Academy demo form using Selenium WebDriver in Python, including entering text, selecting radio buttons and checkboxes, and handling form fields?**

# CODE : 

```PY

from selenium import webdriver
from selenium.webdriver.common.by import By
import time

driver = webdriver.Edge()
driver.maximize_window()

driver.get("https://vinothqaacademy.com/demo-site/")

time.sleep(5)

firstname = driver.find_element(
    By.ID, "vfb-5"
)

firstname.send_keys("Tamizhselvan")

time.sleep(2)

lastname = driver.find_element(
    By.ID, "vfb-7"
)

lastname.send_keys("B")

time.sleep(2)

gender = driver.find_element(
    By.ID, "vfb-31-1"   
)
gender.click()
time.sleep(2)

course = driver.find_element(
    By.ID, "vfb-20-0"
)
course.click()
time.sleep(2)


address = driver.find_element(
    By.ID, "vfb-13-address"
)
address.send_keys("No. 2,1st Street, Thiruvalluvar Nagar")
time.sleep(2)


city = driver.find_element(
    By.ID, "vfb-13-city"
)
city.send_keys("Chennai")
time.sleep(2)

zip_code = driver.find_element(
    By.ID, "vfb-13-zip"
)
zip_code.send_keys("600026")
time.sleep(2)



state = driver.find_element(
    By.ID, "vfb-13-state"  
)
state.send_keys("Tamil Nadu")
time.sleep(2)





email = driver.find_element(
    By.ID, "vfb-14"
)
email.send_keys("sridhartamizh02@gmail.com")
time.sleep(20)
```

### Output :

 <img width="1917" height="1072" alt="image" src="https://github.com/user-attachments/assets/6e9c57fe-7181-49ac-831c-96b789db57e7" />

