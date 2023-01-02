
# Tkinter

```python
import tkinter as tk
from tkinter import ttk

# To check if tkinter is working or not
#tkinter._test();

#Create a root element
root = tk.Tk()

#Adds a label
#ttk.Label(root, text="hello world", padding=(30, 10)).pack()

def greeting():
    print("example")

greet_button = ttk.Button(root, text="Submit", command=greeting)
greet_button.pack()
root.mainloop()
```