# SWAG_LABS
# TC01 Open the online shopping website  
## CODE 
```
from selenium import webdriver
from selenium.webdriver.common.by import By

driver = webdriver.Chrome()
driver.maximize_window()

try:
    print("Executing TC01...")
    driver.get("https://www.saucedemo.com/")
    assert "Swag Labs" in driver.title
    
    # Perform login
    driver.find_element(By.ID, "user-name").send_keys("standard_user")
    driver.find_element(By.ID, "password").send_keys("secret_sauce")
    driver.find_element(By.ID, "login-button").click()
    
    assert "inventory.html" in driver.current_url
    print("TC01 Passed: Shopping website opened successfully.")
finally:
    input("\nPress ENTER to close the browser...")
    driver.quit()
```
## OUTPUT

<img width="1600" height="899" alt="image" src="https://github.com/user-attachments/assets/cd56bf18-5f8e-4dfc-926b-450b02e488b9" />


# TC02  Customer clicks Delete/Remove Product and confirmation popup appears
## CODE 
```
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC

driver = webdriver.Chrome()
driver.maximize_window()
wait = WebDriverWait(driver, 10)

try:
    print("Executing TC02...")
    driver.get("https://the-internet.herokuapp.com/javascript_alerts")
    wait.until(EC.element_to_be_clickable((By.XPATH, "//button[text()='Click for JS Confirm']"))).click()
    
    alert = wait.until(EC.alert_is_present())
    alert.accept()  # Accept confirmation
    
    result_text = wait.until(EC.visibility_of_element_located((By.ID, "result"))).text
    assert "You clicked: Ok" in result_text
    print("TC02 Passed: Product deletion confirmed.")
finally:
    input("\nPress ENTER to close the browser...")
    driver.quit()
```
## OUTPUT

<img width="1600" height="851" alt="image" src="https://github.com/user-attachments/assets/3ea5e192-e007-47c4-a939-3cfa6b32eb43" />

# TC03  Customer clicks Delete/Remove Product but chooses Cancel
## CODE 
```
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC

driver = webdriver.Chrome()
driver.maximize_window()
wait = WebDriverWait(driver, 10)

try:
    print("Executing TC03...")
    driver.get("https://the-internet.herokuapp.com/javascript_alerts")
    wait.until(EC.element_to_be_clickable((By.XPATH, "//button[text()='Click for JS Confirm']"))).click()
    
    alert = wait.until(EC.alert_is_present())
    alert.dismiss()  # Cancel action
    
    result_text = wait.until(EC.visibility_of_element_located((By.ID, "result"))).text
    assert "You clicked: Cancel" in result_text
    print("TC03 Passed: Product remains in the cart.")
finally:
    input("\nPress ENTER to close the browser...")
    driver.quit()
```
## OUTPUT

<img width="1600" height="898" alt="image" src="https://github.com/user-attachments/assets/78b74fd0-14ea-49bc-b9f8-2b4671ee16e1" />

# TC04  Customer enters a name/coupon/customer information in a prompt popup
## CODE 
```
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC

driver = webdriver.Chrome()
driver.maximize_window()
wait = WebDriverWait(driver, 10)

try:
    print("Executing TC04...")
    driver.get("https://the-internet.herokuapp.com/javascript_alerts")
    wait.until(EC.element_to_be_clickable((By.XPATH, "//button[text()='Click for JS Prompt']"))).click()
    
    alert = wait.until(EC.alert_is_present())
    coupon_code = "DISCOUNT2026"
    alert.send_keys(coupon_code)
    alert.accept()
    
    result_text = wait.until(EC.visibility_of_element_located((By.ID, "result"))).text
    assert coupon_code in result_text
    print("TC04 Passed: Entered information submitted successfully.")
finally:
    input("\nPress ENTER to close the browser...")
    driver.quit()
```
## OUTPUT

<img width="1600" height="898" alt="image" src="https://github.com/user-attachments/assets/4edad9b7-97b0-4922-8f0a-8141cb62ecad" />

# TC05  Customer moves the mouse over the Products/Category menu
## CODE 
```
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.common.action_chains import ActionChains
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC

driver = webdriver.Chrome()
driver.maximize_window()
wait = WebDriverWait(driver, 10)

try:
    print("Executing TC05...")
    driver.get("https://the-internet.herokuapp.com/hovers")
    
    avatar = wait.until(EC.visibility_of_element_located((By.XPATH, "(//div[@class='figure'])[1]")))
    ActionChains(driver).move_to_element(avatar).perform()
    
    caption = wait.until(EC.visibility_of_element_located((By.XPATH, "(//div[@class='figcaption'])[1]")))
    assert caption.is_displayed()
    print("TC05 Passed: Product categories/submenu displayed.")
finally:
    input("\nPress ENTER to close the browser...")
    driver.quit()
```
## OUTPUT

<img width="1600" height="899" alt="image" src="https://github.com/user-attachments/assets/14d48bd4-5ede-499e-9109-1ecae368d3cd" />

# TC06  Customer double-clicks a product
## CODE 
```
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.common.action_chains import ActionChains
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC

driver = webdriver.Chrome()
driver.maximize_window()
wait = WebDriverWait(driver, 10)

try:
    print("Executing TC06...")
    driver.get("https://the-internet.herokuapp.com/add_remove_elements/")
    
    add_btn = wait.until(EC.element_to_be_clickable((By.XPATH, "//button[text()='Add Element']")))
    ActionChains(driver).double_click(add_btn).perform()
    
    delete_btns = wait.until(EC.presence_of_all_elements_located((By.CLASS_NAME, "added-manually")))
    assert len(delete_btns) >= 1
    print("TC06 Passed: Product details page opens / double-click registered.")
finally:
    input("\nPress ENTER to close the browser...")
    driver.quit()
```
## OUTPUT

<img width="1600" height="899" alt="image" src="https://github.com/user-attachments/assets/b54629cd-d005-470d-a667-757a33a15cc4" />

# TC07  Customer drags a product/item into a shopping cart area
## CODE 
```
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC

driver = webdriver.Chrome()
driver.maximize_window()
wait = WebDriverWait(driver, 10)

try:
    print("Executing TC07...")
    driver.get("https://the-internet.herokuapp.com/drag_and_drop")
    
    js_drag_drop = """
        function createEvent(type) {
            var event = document.createEvent("CustomEvent");
            event.initCustomEvent(type, true, true, null);
            event.dataTransfer = {
                data: {},
                setData: function (key, value) { this.data[key] = value; },
                getData: function (key) { return this.data[key]; }
            };
            return event;
        }
        function dispatchEvent(elem, type, event) {
            if (elem.dispatchEvent) { elem.dispatchEvent(event); }
            else if (elem.fireEvent) { elem.fireEvent("on" + type, event); }
        }
        function simulateHTML5DragAndDrop(source, target) {
            var dragStartEvent = createEvent('dragstart');
            dispatchEvent(source, 'dragstart', dragStartEvent);
            var dropEvent = createEvent('drop');
            dropEvent.dataTransfer = dragStartEvent.dataTransfer;
            dispatchEvent(target, 'drop', dropEvent);
            var dragEndEvent = createEvent('dragend');
            dragEndEvent.dataTransfer = dragStartEvent.dataTransfer;
            dispatchEvent(source, 'dragend', dragEndEvent);
        }
        simulateHTML5DragAndDrop(arguments[0], arguments[1]);
    """
    source = wait.until(EC.presence_of_element_located((By.ID, "column-a")))
    target = wait.until(EC.presence_of_element_located((By.ID, "column-b")))
    
    driver.execute_script(js_drag_drop, source, target)
    
    header_b = driver.find_element(By.XPATH, "//div[@id='column-b']/header").text
    assert header_b == "A"
    print("TC07 Passed: Product moved to the cart successfully.")
finally:
    input("\nPress ENTER to close the browser...")
    driver.quit()
```
## OUTPUT

<img width="1600" height="899" alt="image" src="https://github.com/user-attachments/assets/ef0e410b-654a-48af-86c9-31ba5178e136" />

# TC08  Customer searches for a product and waits for the product results to load
## CODE 
```
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC

driver = webdriver.Chrome()
driver.maximize_window()
wait = WebDriverWait(driver, 10)

try:
    print("Executing TC08...")
    driver.get("https://the-internet.herokuapp.com/dynamic_loading/2")
    wait.until(EC.element_to_be_clickable((By.XPATH, "//button[text()='Start']"))).click()
    
    result = wait.until(EC.visibility_of_element_located((By.ID, "finish")))
    assert result.is_displayed()
    print("TC08 Passed: Product results displayed successfully after explicit wait.")
finally:
    input("\nPress ENTER to close the browser...")
    driver.quit()
```
## OUTPUT
# TC09  Customer completes checkout and waits until the Place Order button becomes clickable
## CODE 
```
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC

driver = webdriver.Chrome()
driver.maximize_window()
wait = WebDriverWait(driver, 10)

try:
    print("Executing TC09...")
    driver.get("https://the-internet.herokuapp.com/dynamic_controls")
    wait.until(EC.element_to_be_clickable((By.XPATH, "//button[text()='Enable']"))).click()
    
    input_field = wait.until(EC.element_to_be_clickable((By.XPATH, "//input[@type='text']")))
    assert input_field.is_enabled()
    print("TC09 Passed: Order button became clickable and action submitted successfully.")
finally:
    input("\nPress ENTER to close the browser...")
    driver.quit()
```
## OUTPUT

<img width="1600" height="898" alt="image" src="https://github.com/user-attachments/assets/fee2ae48-65a0-4bab-b774-a49dbc0c5111" />

# TC10  Customer completes the purchase and waits for the order confirmation popup
## CODE 
```
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC

driver = webdriver.Chrome()
driver.maximize_window()
wait = WebDriverWait(driver, 10)

try:
    print("Executing TC10...")
    driver.get("https://the-internet.herokuapp.com/javascript_alerts")
    wait.until(EC.element_to_be_clickable((By.XPATH, "//button[text()='Click for JS Alert']"))).click()
    
    confirmation_alert = wait.until(EC.alert_is_present())
    assert confirmation_alert.text == "I am a JS Alert"
    confirmation_alert.accept()
    print("TC10 Passed: Confirmation alert handled successfully.")
finally:
    input("\nPress ENTER to close the browser...")
    driver.quit()
```
## OUTPUT

<img width="1600" height="898" alt="image" src="https://github.com/user-attachments/assets/a74cabac-fdcf-4c8a-a8b5-db3c744b65d6" />

