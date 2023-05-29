# Carryout
import time
from selenium.webdriver.common.by import By
from selenium import webdriver
from selenium.webdriver.chrome.options import Options
options=webdriver.ChromeOptions()
options.add_experimental_option("detach",True)
driver=webdriver.Chrome(options=options)
driver.get("https://order-qa.your-buddy.com/#/rt/menu?oi=1&bi=20221222113912386740&dm=takeaway&mci=mci-2020&js=l9lBlr4AeZquvSBbPAefg7z4KCwOTcHagBlCc1BB%20B1fn%2FVztw607KjvmztNB3Duq%20rI4%2FgIN1hDTUYNp%2F0u%2F4MoT3svtbWXB37D58arto4UStZuRrDe8hx1d29yGKauIc%2Fxw3WQgQ3AmeF05AO8d3nN8sw9IYPe%2Fk0nmS826CZ8X87tq7Gdkuyx5Vc7iDi%2FmAeMzTDMI4sCKzEHnXCoIZxUomzJ3dtO1O%20lh9PDnfQKSiG4I3B%20RLYUsbiYae4nPolYkAGcaBiZT%207L5JdJ2kURenwyXLpQKFVkVqsoLTgNhyoMUYTTenthkB8TE1DWPDBPc1Vr9si%20UsOL%20b36yQt0%20cfrpWvqBx0P1IB%2FF7G5p%20Zc3PO8JQtyQQpn3rTAT1IzF0r%20WgPxeizzpcktfzN%20jqU93kLlM3ln0E9zNxcR%20sKobJd5%2FtN5Fml6tBV2LONIjlLepR%20e%2Fpu0L40dYbyYPmHGA3G7D5AhX4Ln5j5%20te9iA24IJG0v5A%20XLh8Z")
def openBrowser():
    #if bType == 'chrome':
     #   driver.get(
      #      "https://order-qa.your-buddy.com/#/rt/menu?oi=1&bi=20221222113912386740&dm=dinein&mci=mci-2020&js=fI49g8LZntK+3BhVuWMeaNxIOi59OTeWM8BduRtJAXBvyO40noOCxWlkGVMLMrQmR30tdIENQ9Fa1xNNULatXXnctaZEyBQ3wdCWNv+qcm7sqF2MylBB5vMm1CYPne7CJ1ZUVQKknuzo4uMkRKjJC7jHKjDHj22WW0zGfu+CNgCDzjBXklerxZJr+Sipd/fBtZB54vWppgBWC+aDoU8EeY/1Z0RTxfjjpPWN+1+cXhzV7HZKRq1rdZUnkRqIcrmi91u8oH2nCDOXL28y7P77wHj0Eoj5uHQSC9TXzpvKPMzwJQTRAr4EDxkRjnWaI8auISxdpM5/1hTVNppT7/WdBQ6hpq74JjIHTN5YAACz7t9PuG/P15QKZIhDC+dY6RHK64YRc/fbI2HmU1FSKBPBjjJaltgm9gWshwaHzI5X98nUgB3xDYoFkrOF9aevWWZnalk1ilqHkc4D3J1kPqhC4F3lWtxwrsWX453NTPgdJnme/k/6KzT66gQHsl/vqK/l")
       # time.sleep(10)
        menucard_select = int(input("Enter Choice: "))
        if menucard_select == 1:
            print(driver.find_element(By.XPATH, "//*[contains(text(), 'English Menu')]").text)
            driver.find_element(By.XPATH, "(//input[@id='item.menu_card_id'])[1]").click()
            time.sleep(4)
        elif menucard_select == 2:
            print(driver.find_element(By.XPATH, "//*[contains(text(), 'española')]").text)
            driver.find_element(By.XPATH, "(//input[@id='item.menu_card_id'])[2]").click()
        elif menucard_select == 3:
            print(driver.find_element(By.XPATH, "//*[contains(text(), 'Русский')]").text)
            driver.find_element(By.XPATH, "(//input[@id='item.menu_card_id'])[3]").click()
        elif menucard_select == 5:
            print(driver.find_element(By.XPATH, "//*[contains(text(), 'عربي')]").text)
            driver.find_element(By.XPATH, "(//input[@id='item.menu_card_id'])[5]").click()
        else:
            print('fail')
        #time.sleep(3)
def item_selection():

    # container
    categories = driver.find_elements(By.XPATH, "//div[starts-with(@class,'arrow')]")

    for category in categories:

        categoryName = category.find_element(By.XPATH,"//div[starts-with(@class,'block-txt-scroll in-block')][5]").text
        #print(category.find_element("//div[starts-with(@class,'block-txt-scroll in-block')]"))
        if categoryName == "Pizza":
            category.find_element(By.XPATH, "//div[starts-with(@class,'block-txt-scroll in-block')][5]").click()
            time.sleep(3)
            print('success')
        else:
            print("There is no category")

def items_adding():
    select_items = input("select the items from the Menu:-")
    list_of_items = []
    cart = 0
    #total items in pizza
    Container=driver.find_elements(By.XPATH,"//div[@class='menu-skeleton']")

    for items in Container:
        #1st element selection
        first_item=items.find_element(By.XPATH,"(//div[@class='menu-name'])[1]").text

        if select_items==first_item:
            items.find_element(By.XPATH, "//div[@class='menu-container-loader']/div/div[1]/div[3]/div/div/div/span[1]/i[1]").click()#1st item selected and clicked
            time.sleep(5)

            print(driver.find_element(By.XPATH,"(//span[@class='cart-items-count'])[1]").text)#cart items
            cart+=1
            print("The cart is:",cart)
            time.sleep(3)

            items.find_element(By.XPATH, "//button[@class='checkoutbtn']").click()
            list_of_items.append(select_items)

            print("The items you have selected:-",list_of_items)

            break
    else:
        print("Fail")
def login():
    number=input("Enter the number:-")
    driver.find_element(By.XPATH, "//input[@type='number']").send_keys(number)
    driver.maximize_window()
    time.sleep(3)
    if len(number) == 10:
        print("Entered correct number...!!!!")
        driver.find_element(By.XPATH, "//input[@type='checkbox']").click()
        driver.find_element(By.XPATH, "//button[@class='submitButn']").click()
    else:

        driver.find_element(By.XPATH, "//input[@type='checkbox']").click()
        driver.find_element(By.XPATH, "//button[@class='submitButn']").click()
        print("Check the mobile number...!!!!")

def otp():

    Otp=input("Enter the OTP:-")
    driver.find_element(By.XPATH, "//input[starts-with(@type,'text')]").send_keys(Otp)
    #time.sleep(5)
    if len(Otp) ==6:

        driver.find_element(By.XPATH,"//button[starts-with(@class,'verifyButn')]").click()
    else:
        print("Enter the valid OTP...!!!!")

openBrowser()
item_selection()
items_adding()
time.sleep(3)
login()
time.sleep(2)
otp()
time.sleep(10)
driver.close()
