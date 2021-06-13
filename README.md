# FloAIO
""" Sneaker Bot
- Generate a url for the specific shoe*
- Check what shoe size is available
- Add to cart and Check out the shoe automatically, if available
- have shipping info saved
- captcha solver
""" 
import time
from selenium import webdriver
from webdriver_manager.chrome import ChromeDriverManager



class Shoe:
    def __init__(self,number,model,sku):
        self.number = number                    #inventory number    
        self.model = model                  #name of shoe 
        self.sku = sku                      #Shoe Serial Number
def footaction(sku,model):          #URL parser for footaction
    listofString = model.split(" ")
    length = len(listofString)
    string = ''
    sku = str(sku)
    i = 0
    while i < length:
        string += listofString[i]
        if i != length -1:
            string += '-'
        i += 1 
    URL = 'https://www.footaction.com/product/' + str(string) + '/' + sku[1:] + '.html'
    return URL
def eastbay(sku,model):             #URL parser for Eastbay.com
    listofString = model.split(" ")
    length = len(listofString)
    string = ''
    sku = str(sku)
    i = 0
    while i < length:
        string += listofString[i]
        if i != length -1:
            string += '-'
        i += 1 
    URL = 'https://www.eastbay.com/product/' + str(string) + '/' + sku[1:] + '.html'
    return URL
def champs(sku,model):                  #URL parser Champs.com                  
    listofString = model.split(" ")
    length = len(listofString)
    string = ''
    sku = str(sku)
    i = 0
    while i < length:
        string += listofString[i]
        if i != length -1:
            string += '-'
        i += 1 
    URL = 'https://www.champssports.com/product/' + str(string) + '/' + sku[1:] + '.html'
    return URL
def footlocker(sku,model):              #URl parser for footlocker.com
    listofString = model.split(" ")
    length = len(listofString)
    string = ''
    sku = str(sku)
    i = 0
    while i < length:
        string += listofString[i]
        if i != length -1:
            string += '-'
        i += 1 
    URL = 'https://www.footlocker.com/product/' + str(string) + '/' + sku[1:] + '.html'
    return URL    
def releases(shoes):            #Gives Output for all shoe models then gives user input
    print('Models:')
    length = len(shoes)
    i = 0
    while i < length:
        dash = "- "
        model = shoes[i]
        a = str(i+1)
        print( a + dash + model)
        i += 1
    number = input("Select the shoe you would like to purchase(Enter number): ")
    int(number)
    return number
def getModel(number,shoelist):
    model = shoelist[int(number) - 1].model
    return model
def getSku(number,shoelist):
    skuNum = shoelist[int(number) - 1].sku    
    return skuNum
s1 = Shoe(1,"Jordan 1 Mid SE",554724092)
s2 = Shoe(2,"Nike air force 1 07 Mens","CJ0952100")
s3 = Shoe(3,"Nike Air VaporMax 2020 Flyknit","CJ6740002")
s4 = Shoe(4,"Air Jordan 4",2309575)
shoelist = [s1,s2,s3,s4]
shoeModels = [s1.model,s2.model,s3.model,s4.model]
shoeNum = releases(shoeModels)
sku = getSku(shoeNum,shoelist) 
model = getModel(shoeNum,shoelist)
statement =  '   ' 
print(sku)
print(model)
eURL = eastbay(sku, model)
faURL = footaction(sku,model)
cURL = champs(sku,model)
flURL = footlocker(sku,model)
print(eURL)
print(faURL)
print(cURL)
print(flURL)

#eastbay driver
eDriver = webdriver.Chrome(ChromeDriverManager().install())
eDriver.maximize_window()
eDriver.get(flURL)  #opens the url
eIdx = 0
while eIdx < 5:

    try:
        #addtoCheckout = addbutton = eDriver.find_element_by_class_name("c-form-field c-form-field--radio c-form-field--disabled c-form-field--unavailable ProductSize")
        addtoCheckout = addbutton = eDriver.find_element_by_link_text("Nike Air Force 1 Low")
        print("sold out.")
        eIdx += 1
        time.sleep(1)
        eDriver.refresh()
    except:
        addtoCheckout = addbutton = eDriver.find_element_by_class_name("c-form-label-content")
        
        print("Checked out...")
        #addtoCheckout.click()
        eIdx = 5

print("Appliction title is ",eDriver.title)
print("Application url is ",eDriver.current_url)
eDriver.quit()
"""
eDriver.get(faURL)
eDriver.get(cURL)
eDriver.get(flURL)


#footaction driver
faDriver = webdriver.Chrome(ChromeDriverManager().install())
faDriver.maximize_window()
faDriver.get(faURL)
print("Appliction title is ",faDriver.title)
print("Application url is ",faDriver.current_url)
faDriver.quit()

#champssports driver
cDriver = webdriver.Chrome(ChromeDriverManager().install())
cDriver.maximize_window()
cDriver.get(cURL)
print("Appliction title is ",cDriver.title)
print("Application url is ",cDriver.current_url)
cDriver.quit()

#foot locker driver
flDriver = webdriver.Chrome(ChromeDriverManager().install())
flDriver.maximize_window()
flDriver.get(flURL)
print("Appliction title is ",flDriver.title)
print("Application url is ",flDriver.current_url)
flDriver.quit()
"""







"""
import tkinter as tk
from tkinter import filedialog,Text
import os

root = tk.Tk()

B = tk.Button(root,text = "Open File",bg = "red",padx= 10,pady =5,fg = "white")
B.pack()
canvas = tk.Canvas(root,height = 700,width = 700, bg = "green")
canvas.pack()
frame = tk.Frame(root,bg ="white")
frame.place(relwidth = 0.8,relheight = 0.8,relx= .1,rely= .1)
root.mainloop()
"""


