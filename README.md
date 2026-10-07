# HCL_Automation_Testing

## 05-10-2026 : 

1. Project 1: Google Search – Open Actor Simbu Search Results 

2. Project 2: SauceDemo Login and Product Listing 

3. Project 3: OTP-Based Login Automation – Flipkart QA Approach 


## 06-10-26  TASK - 1: 

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

firstname = driver.find_element(By.ID, "vfb-5")
firstname.send_keys("Tamizhselvan")
time.sleep(2)

lastname = driver.find_element(By.ID, "vfb-7")
lastname.send_keys("B")
time.sleep(2)

gender = driver.find_element(By.ID, "vfb-31-1")
gender.click()
time.sleep(2)

course = driver.find_element(By.ID, "vfb-20-0")
course.click()
time.sleep(2)

address = driver.find_element(By.ID, "vfb-13-address")
address.send_keys("No. 2,1st Street, Thiruvalluvar Nagar")
time.sleep(2)

city = driver.find_element(By.ID, "vfb-13-city")
city.send_keys("Chennai")
time.sleep(2)

zip_code = driver.find_element(By.ID, "vfb-13-zip")
zip_code.send_keys("600026")
time.sleep(2)

state = driver.find_element(By.ID, "vfb-13-state")
state.send_keys("Tamil Nadu")
time.sleep(2)

email = driver.find_element(By.ID, "vfb-14")
email.send_keys("sridhartamizh02@gmail.com")
time.sleep(20)
```

### Output :

 <img width="1917" height="1072" alt="image" src="https://github.com/user-attachments/assets/6e9c57fe-7181-49ac-831c-96b789db57e7" />


## 06-10-26  TASK - 2: 

### 2. How can I automate Amazon login, search for men’s shoes, add a product to the cart, proceed to checkout, and select a payment method using Selenium with Python?

```


from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC
import time

driver = webdriver.Edge()
driver.maximize_window()

wait = WebDriverWait(driver, 20)
driver.get("https://www.amazon.in/")


login = wait.until(EC.element_to_be_clickable((By.CLASS_NAME, "nav-line-1-container")))
login.click()

phone = wait.until(EC.visibility_of_element_located((By.NAME, "email")))
phone.send_keys("9943235660")

cont = wait.until(EC.element_to_be_clickable((By.CLASS_NAME, "a-button-input")))
cont.click()

otp = wait.until(EC.visibility_of_element_located((By.NAME, "code")))
otp.send_keys(input("Enter OTP: "))

otp_button = wait.until(EC.element_to_be_clickable((By.CLASS_NAME, "a-button-input")))
otp_button.click()

print("Login successful")

search = wait.until(EC.visibility_of_element_located((By.ID, "twotabsearchtextbox")))
search.send_keys("Mens shoes")


search_button = wait.until(EC.element_to_be_clickable((By.ID, "nav-search-submit-button")))
search_button.click()
print("Product searched")
time.sleep(4)


buttons = driver.find_elements(By.XPATH, '//button[@aria-label="Add to cart"]')
print("Add to cart buttons found:", len(buttons))


for button in buttons:
    if button.is_displayed() and button.is_enabled():
        driver.execute_script("arguments[0].scrollIntoView({block: 'center'});",button)
        time.sleep(1)
        button.click()
        print("Product added to cart")
        break
else:
    print("No enabled Add to cart button found.")

time.sleep(3)
driver.get("https://www.amazon.in/gp/cart/view.html")
print("Cart opened")
time.sleep(4)


checkout = wait.until(EC.element_to_be_clickable((By.NAME, "proceedToRetailCheckout")))
checkout.click()
print("Checkout opened")
time.sleep(5)

try:
    payment = wait.until(EC.element_to_be_clickable((By.NAME, "ppw-instrumentRowSelection")))
    payment.click()
    print("Payment method selected")
except:
    print("Payment method was not found")

input("Press Enter to close browser...")
driver.quit()



```

### OUTPUT :

<img width="1917" height="1078" alt="image" src="https://github.com/user-attachments/assets/07dd4fee-ab8f-4a25-9207-bf483f0b5c2c" />

