# tempconverter
import sys
 
from PyQt5.QtWidgets import QApplication, QWidget, QPushButton, QLabel, QGridLayout, QLineEdit
from PyQt5.QtCore import Qt
#from PyQt5.QtGui import QIcon


class Calculator(QWidget):
    def __init__(self):
        super().__init__()
        self.pretemp_selected = 0
        self.post_temp_selected = 0
        self.oooioi = "kevin durant"
        self.input_textbox = QLineEdit(self)
        self.pretemp_celcius = QPushButton("C°", self)
        self.pretemp_farenheit = QPushButton("F°", self)
        self.pretemp_kelvin = QPushButton("K°", self)
        self.post_temp_celcius = QPushButton("C°", self)
        self.post_temp_farenheit = QPushButton("F°", self)
        self.post_temp_kelvin = QPushButton("K°", self)
        self.button_enter = QPushButton("GET TEMPERATURE CONVERTED", self)
        self.button_help = QPushButton("Help", self)
        self.titlelabel = QLabel("TEMPERATURE CONVERTER", self)
        self.initUI()


    def initUI(self):
        gridlayout = QGridLayout()
        self.input_textbox.setPlaceholderText("ENTER TEMPERATURE")
        self.setWindowTitle("Temperature Converter")
        gridlayout.addWidget(self.titlelabel,0,0,1,3)
        gridlayout.addWidget(self.pretemp_kelvin,1,0)
        gridlayout.addWidget(self.pretemp_celcius,1,1)
        gridlayout.addWidget(self.pretemp_farenheit,1,2)
        gridlayout.addWidget(self.input_textbox,2,0,1,3)
        gridlayout.addWidget(self.post_temp_kelvin,3,0)
        gridlayout.addWidget(self.post_temp_celcius,3,1)
        gridlayout.addWidget(self.post_temp_farenheit,3,2)
        gridlayout.addWidget(self.button_enter,4,0,1,2)
        gridlayout.addWidget(self.button_help,4,2,1,1)
        self.titlelabel.setAlignment(Qt.AlignHCenter)
        self.setLayout(gridlayout)


        self.pretemp_kelvin.clicked.connect(self.kelvin_clicked)
        self.pretemp_celcius.clicked.connect(self.celcius_clicked)
        self.pretemp_farenheit.clicked.connect(self.farenheit_clicked)
        self.post_temp_kelvin.clicked.connect(self.post_kelvin_clicked)
        self.post_temp_celcius.clicked.connect(self.post_celcius_clicked)
        self.post_temp_farenheit.clicked.connect(self.post_farenheit_clicked)
        self.button_enter.clicked.connect(self.display)
        self.button_help.clicked.connect(self.help)



    def kelvin_clicked(self):
        self.pretemp_selected = 1
        self.pretemp_kelvin.setStyleSheet("background-color: #000830; color: white;")
        self.pretemp_celcius.setStyleSheet("")
        self.pretemp_farenheit.setStyleSheet("")


    def celcius_clicked(self):
        self.pretemp_selected = 2
        self.pretemp_kelvin.setStyleSheet("")
        self.pretemp_celcius.setStyleSheet("background-color: #000830; color: white;")
        self.pretemp_farenheit.setStyleSheet("")

    def farenheit_clicked(self):
        self.pretemp_selected = 3
        self.pretemp_kelvin.setStyleSheet("")
        self.pretemp_celcius.setStyleSheet("")
        self.pretemp_farenheit.setStyleSheet("background-color: #000830; color: white;")




#--------------------POST---------------------------#



    def post_kelvin_clicked(self):
        self.post_temp_selected = 1
        self.post_temp_kelvin.setStyleSheet("background-color: #000830; color: white;")
        self.post_temp_celcius.setStyleSheet("")
        self.post_temp_farenheit.setStyleSheet("")

    def post_celcius_clicked(self):
        self.post_temp_selected = 2
        self.post_temp_kelvin.setStyleSheet("")
        self.post_temp_celcius.setStyleSheet("background-color: #000830; color: white;")
        self.post_temp_farenheit.setStyleSheet("")

    def post_farenheit_clicked(self):
        self.post_temp_selected = 3
        self.post_temp_kelvin.setStyleSheet("")
        self.post_temp_celcius.setStyleSheet("")
        self.post_temp_farenheit.setStyleSheet("background-color: #000830; color: white;")



#---------------------------------------------------------


    def display(self):
        if self.post_temp_selected == 1:
            converted_temp = self.convert_to_kelvin(int(self.input_textbox.text()), self.pretemp_selected)
        elif self.post_temp_selected == 2:
            converted_temp = self.convert_to_celcius(int(self.input_textbox.text()), self.pretemp_selected)
        elif self.post_temp_selected == 3:
            converted_temp = self.convert_to_farenheit(int(self.input_textbox.text()), self.pretemp_selected)

        self.titlelabel.setText(str(converted_temp))

    def help(self):
        self.titlelabel.setText("1st row for current temperature 2nd row to convert")

    @staticmethod
    def convert_to_kelvin(temp,pre):
        if pre == 1:
            return temp + 273.15
        elif pre == 3:
            return (temp * (9/5)) + 32
        else:
            return temp

    @staticmethod
    def convert_to_celcius(temp,pre):
        if pre == 1:
            return temp - 273.15
        elif pre == 3:
            return (temp - 32) * (5/9)
        else:
            return temp


    @staticmethod
    def convert_to_farenheit(temp,pre):
        if pre == 1:
            return (temp - 273.15) * (9/5) + 35
        elif pre == 2:
            return (temp * (9/5)) + 32
        else:
            return temp














if __name__ == '__main__':
    app = QApplication(sys.argv)
    calc = Calculator()
    calc.show()
    sys.exit(app.exec_())
