# PyQt5 Note

> @ wyfffffei
>
> official: https://doc.qt.io/qt-6/designer-quick-start.html
> qt designer: http://www.codebaoku.com/it-c/it-c-219841.html
> tutorial: https://www.jc2182.com/pyqt5/pyqt5-designer.html



## 基础配置

- 环境配置

```bash
pip install -i https://pypi.tuna.tsinghua.edu.cn/simple PyQt5 pyqt5-tools
```

- `ui`文件打包

```bash
pyuic5 -x demo.ui -o demo.py
```



## 简单demo

- click event

```python
import sys
from PyQt5.QtCore import *
from PyQt5.QtGui import *
from PyQt5.QtWidgets import *

def window():
   app = QApplication(sys.argv)
   win = QDialog()
   b1 = QPushButton(win)
   b1.setText("Button1")
   b1.move(50,20)
   b1.clicked.connect(b1_clicked)
   
   b2 = QPushButton(win)
   b2.setText("Button2")
   b2.move(50,50)
   b2.clicked.connect(b2_clicked)
   
   win.setGeometry(100,100,200,100)

   win.setWindowTitle("PyQt5")
   win.show()
   sys.exit(app.exec_())

def b1_clicked():
   print ("Button 1 clicked")

def b2_clicked():
   print ("Button 2 clicked")

if __name__ == '__main__':
   window()

```

- drag event

```python
import sys
from PyQt5.QtCore import *
from PyQt5.QtGui import *
from PyQt5.QtWidgets import *

class combo(QComboBox):
   def __init__(self, title, parent):
      super(combo, self).__init__( parent)
      self.setAcceptDrops(True)

   def dragEnterEvent(self, e):
      print (e)

      if e.mimeData().hasText():
         e.accept()
      else:
         e.ignore()

   def dropEvent(self, e):
      self.addItem(e.mimeData().text())

class Example(QWidget):
   def __init__(self):
      super(Example, self).__init__()

      self.initUI()

   def initUI(self):
      lo = QFormLayout()
      lo.addRow(QLabel("Type some text in textbox and drag it into combo box"))
   
      edit = QLineEdit()
      edit.setDragEnabled(True)
      com = combo("Button", self)
      lo.addRow(edit,com)
      self.setLayout(lo)
      self.setWindowTitle('Simple drag and drop')
def main():
   app = QApplication(sys.argv)
   ex = Example()
   ex.show()
   app.exec_()

if __name__ == '__main__':
   main()

```

