import os
import sys
import requests
from PyQt5.QtGui import QPixmap
from PyQt5.QtWidgets import QApplication, QWidget, QLabel

SCREEN_SIZE = [600, 450]
scale = 0.002
long = 37.530887
lat = 55.703118


class Example(QWidget):
    def __init__(self):
        super().__init__()
        self.initUI()
        self.getImage()


    def getImage(self):
        #global scale
        map_request = "http://static-maps.yandex.ru/1.x/?ll={},{}&spn={},{}&l=map".format(long, lat, scale, scale)
        response = requests.get(map_request)

        if not response:
            print("Ошибка выполнения запроса:")
            print(map_request)
            print("Http статус:", response.status_code, "(", response.reason, ")")
            sys.exit(1)

        # Запишем полученное изображение в файл.
        self.map_file = "map.png"
        with open(self.map_file, "wb") as file:
            file.write(response.content)

        self.pixmap = QPixmap(self.map_file)

        self.image.setPixmap(self.pixmap)


    def keyPressEvent(self, event):
        global scale
        global long
        global lat
        print("pressed key " + str(event.key()))
        if event.key() == 16777238:
            print("page up")
            if scale < 90:
                scale += 0.002
            self.getImage()
        if event.key() == 16777239:
            print("page down")
            if scale > 0.002:
                 scale -= 0.002
            self.getImage()
        # if event.key() == 16777235:
        #     if long < 180:
        #         long += scale
        #     self.getImage()
        # if event.key() == 16777237:
        #     if long > 0:
        #         long -= scale
        #     self.getImage()
        # if event.key() == 16777236:
        #     if lat > 0:
        #         lat -= scale
        #     self.getImage()
        # if event.key() == 16777234:
        #     if lat < 180:
        #         lat += scale
        #     self.getImage()




    def initUI(self):
        self.setGeometry(100, 100, *SCREEN_SIZE)
        self.setWindowTitle('Отображение карты')

        ## Изображение
        self.image = QLabel(self)
        self.image.move(0, 0)
        self.image.resize(600, 450)


    def closeEvent(self, event):
        """При закрытии формы подчищаем за собой"""
        os.remove(self.map_file)


if __name__ == '__main__':
    app = QApplication(sys.argv)
    ex = Example()
    ex.show()
    sys.exit(app.exec())
