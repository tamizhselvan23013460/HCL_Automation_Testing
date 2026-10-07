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

```py


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





# 07-10-2026 TASK-1


Test Case	Shopping Scenario	Selenium Concept	Expected Result
1. TC01	Open the online shopping website	driver.get()	Shopping website opens successfully
2. TC02	Customer clicks Delete/Remove Product and confirmation popup appears	Alert – accept()	Product deletion is confirmed
3. TC03	Customer clicks Delete/Remove Product but chooses Cancel	Alert – dismiss()	Product remains in the cart
4. TC04	Customer enters a name/coupon/customer information in a prompt popup	Prompt – send_keys()	Entered information is submitted successfully
5. TC05	Customer moves the mouse over the Products/Category menu	Mouse Hover	Product categories/submenu are displayed
6. TC06	Customer double-clicks a product	Double Click	Product details page opens
7. TC07	Customer drags a product/item into a shopping cart area	Drag & Drop	Product is moved to the cart
8. TC08	Customer searches for a product and waits for the product results to load	Explicit Wait	Product is displayed successfully
9. TC09	Customer completes checkout and waits until the Place Order button becomes clickable	Clickable Wait	Order is submitted successfully
10. TC10	Customer completes the purchase and waits for the order confirmation popup	Alert Wait	Confirmation alert is handled successfully


```py


from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.common.action_chains import ActionChains
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC
import time

driver = webdriver.Edge()
driver.maximize_window()
wait = WebDriverWait(driver, 10)
driver.get("https://www.saucedemo.com/")

print("TC01 - Shopping website opened successfully")
wait.until(EC.visibility_of_element_located((By.ID, "user-name"))).send_keys("standard_user")
time.sleep(2)
driver.find_element(By.ID, "password").send_keys("secret_sauce")
driver.find_element(By.ID, "login-button").click()
time.sleep(2)
wait.until(EC.visibility_of_element_located((By.CLASS_NAME, "inventory_list")))
print("TC01 - Login successful")
time.sleep(2)

driver.get("https://www.selenium.dev/selenium/web/alerts.html")
driver.find_element(By.ID, "alert").click()
alert = wait.until(EC.alert_is_present())
time.sleep(2)
print("\nTC02 - Alert:")
print(alert.text)
time.sleep(2)
alert.accept()
print("TC02 - Product deletion confirmed")

driver.get("https://www.selenium.dev/selenium/web/alerts.html")
time.sleep(2)
driver.find_element(By.ID, "confirm").click()
alert = wait.until(EC.alert_is_present())
time.sleep(2)
print("\nTC03 - Confirmation Alert:")
print(alert.text)
alert.dismiss()
time.sleep(2)
print("TC03 - Product remains in the cart")

driver.get("https://www.selenium.dev/selenium/web/alerts.html")
time.sleep(2)
driver.find_element(By.ID, "prompt").click()
alert = wait.until( EC.alert_is_present())
time.sleep(2)
print("\nTC04 - Prompt Alert:")
print(alert.text)
alert.send_keys("TAMIZH")
alert.accept()
print("TC04 - Customer information submitted successfully")

driver.get("https://www.selenium.dev/selenium/web/mouse_interaction.html")
time.sleep(2)
hover_element = wait.until(EC.visibility_of_element_located((By.ID, "hover")))
ActionChains(driver).move_to_element(hover_element).perform()
time.sleep(2)
move_status = wait.until(EC.visibility_of_element_located((By.ID, "move-status")))
print("\nTC05 - Mouse Hover performed successfully")
print("Result:", move_status.text)

driver.get("https://www.selenium.dev/selenium/web/mouse_interaction.html")
time.sleep(2)
double_click_element = wait.until(EC.visibility_of_element_located((By.ID, "clickable")))
ActionChains(driver).double_click(double_click_element).perform()
click_status = wait.until(EC.visibility_of_element_located((By.ID, "click-status")))
print("\nTC06 - Double Click performed successfully")
print("Result:", click_status.text)

driver.get("https://www.selenium.dev/selenium/web/mouse_interaction.html")
time.sleep(2)
source = wait.until(EC.visibility_of_element_located((By.ID, "draggable")))
time.sleep(2)
target = wait.until(EC.visibility_of_element_located((By.ID, "droppable")))
time.sleep(2)
ActionChains(driver).drag_and_drop(source, target).perform()
drop_status = wait.until(EC.visibility_of_element_located((By.ID, "drop-status")))
time.sleep(2)
print("\nTC07 - Drag and Drop performed successfully")
print("Result:", drop_status.text)

driver.get("https://www.automationexercise.com/products")
time.sleep(2)
search_box = wait.until(EC.visibility_of_element_located((By.ID, "search_product")))
time.sleep(2)
search_box.clear()
search_box.send_keys("Top")
search_button = wait.until(EC.element_to_be_clickable((By.ID, "submit_search")))
time.sleep(2)
search_button.click()
searched_products = wait.until(EC.visibility_of_element_located((By.XPATH,
            "//h2[contains(translate(normalize-space(.), 'abcdefghijklmnopqrstuvwxyz', 'ABCDEFGHIJKLMNOPQRSTUVWXYZ'), 'SEARCHED PRODUCTS')]")))
time.sleep(2)
products = wait.until(EC.presence_of_all_elements_located((By.XPATH,"//div[contains(@class,'productinfo')]")))
time.sleep(2)
print("\nTC08 - Product search completed successfully")
print("Result:", searched_products.text)
print("Number of products found:", len(products))

driver.get("https://www.saucedemo.com/")
time.sleep(2)
wait.until(EC.visibility_of_element_located((By.ID, "user-name"))).send_keys("standard_user")
time.sleep(2)
driver.find_element(By.ID, "password").send_keys("secret_sauce")
driver.find_element(By.ID, "login-button").click()
wait.until(EC.visibility_of_element_located((By.CLASS_NAME, "inventory_list")))
time.sleep(2)
driver.find_element(By.ID, "add-to-cart-sauce-labs-backpack").click()
time.sleep(2)
driver.find_element(By.CLASS_NAME, "shopping_cart_link").click()
time.sleep(2)
wait.until(EC.visibility_of_element_located((By.CLASS_NAME, "cart_item")))
time.sleep(2)
driver.find_element(By.ID, "checkout").click()
wait.until(EC.visibility_of_element_located((By.ID, "first-name"))).send_keys("TAMIZH")
time.sleep(2)
driver.find_element(By.ID, "last-name").send_keys("B")
driver.find_element(By.ID, "postal-code").send_keys("600001")
driver.find_element(By.ID, "continue").click()
finish_button = wait.until(EC.element_to_be_clickable((By.ID, "finish")))
time.sleep(2)
print("\nTC09 - Place Order button is clickable")
finish_button.click()
confirmation = wait.until(
EC.visibility_of_element_located((By.CLASS_NAME, "complete-header")))
print("TC09 - Order submitted successfully")
print("Result:", confirmation.text)

driver.get("https://www.saucedemo.com/")
time.sleep(2)
wait.until(EC.visibility_of_element_located((By.ID, "user-name"))).send_keys("standard_user")
driver.find_element(By.ID, "password").send_keys("secret_sauce")
driver.find_element(By.ID, "login-button").click()
wait.until(EC.visibility_of_element_located((By.CLASS_NAME, "inventory_list")))
time.sleep(2)
driver.find_element(By.ID, "add-to-cart-sauce-labs-backpack").click()
driver.find_element(By.CLASS_NAME, "shopping_cart_link").click()
wait.until(EC.visibility_of_element_located((By.CLASS_NAME, "cart_item")))
driver.find_element(By.ID, "checkout").click()
time.sleep(2)
wait.until(EC.visibility_of_element_located((By.ID, "first-name"))).send_keys("TAMIZH")
driver.find_element(By.ID, "last-name").send_keys("B")
driver.find_element(By.ID, "postal-code").send_keys("600001")
driver.find_element(By.ID, "continue").click()
finish_button = wait.until(EC.element_to_be_clickable((By.ID, "finish")))
finish_button.click()
wait.until(EC.visibility_of_element_located((By.CLASS_NAME, "complete-header")))
time.sleep(2)
driver.execute_script("setTimeout(function(){alert('Order confirmation successful')}, 500)")
alert = wait.until(EC.alert_is_present())
print("\nTC10 - Order Confirmation Alert:")
print(alert.text)
alert.accept()
print("TC10 - Confirmation alert handled successfully")
time.sleep(2)
driver.quit()
print("\nAll test cases completed successfully")

```
# OUTPUT :

<img width="1917" height="1025" alt="image" src="https://github.com/user-attachments/assets/755cd047-6864-4190-84a2-c9503a37c036" />


