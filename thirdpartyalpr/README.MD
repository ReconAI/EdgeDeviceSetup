# Thrid-Party ALPR Libraries installation fuides

## OpenALPR
[Site](https://github.com/openalpr/openalpr)

### Installation instruction
[Medium](https://medium.com/@alannewcomer/license-plate-recognition-with-a-jetson-nano-e94c6ff683bc)

1. Get leptonica from:
'http://www.leptonica.org/source/leptonica-1.78.0.tar.gz'

### [Helpful instruction](https://github.com/openalpr/openalpr/issues/660)

Add the tesseract PPA to your repo list
sudo add-apt-repository ppa:alex-p/tesseract-ocr -y
sudo apt-get update -y

Reinstall tesseract
sudo apt-get purge libtesseract-dev
sudo apt-get install libtesseract-dev

2. Install Python library from sources:

```sh
cd openalpr/src/bindings/python/
sudo python3 setup.py install
```


### Test the library
```sh
wget http://plates.openalpr.com/ea7the.jpg
alpr -c us ea7the.jpg

wget http://plates.openalpr.com/h786poj.jpg
alpr -c eu h786poj.jpg
```

### Troubleshooting

In case of 'Error opening data file /usr/share/openalpr/runtime_data/ocr/lus.traineddata ... TESSDATA_PREFIX ...':

```sh
sudo cp -a /usr/share/openalpr/runtime_data/ocr/tessdata/*.traineddata /usr/share/openalpr/runtime_data/ocr/
```

### [Python binding](http://doc.openalpr.com/bindings.html#python)

Usage example:
```sh
from openalpr import Alpr

alpr = Alpr("us", "/path/to/openalpr.conf", "/path/to/runtime_data")
if not alpr.is_loaded():
    print("Error loading OpenALPR")
    sys.exit(1)

alpr.set_top_n(20)
alpr.set_default_region("md")

results = alpr.recognize_file("/path/to/image.jpg")

i = 0
for plate in results['results']:
    i += 1
    print("Plate #%d" % i)
    print("   %12s %12s" % ("Plate", "Confidence"))
    for candidate in plate['candidates']:
        prefix = "-"
        if candidate['matches_template']:
            prefix = "*"

        print("  %s %12s%12f" % (prefix, candidate['plate'], candidate['confidence']))

# Call when completely done to release memory
alpr.unload()
```

On Linux systems, the default paths for files required to instantiate the Alpr class are: <br>
1. /etc/openalpr/openalpr.conf
2. /usr/share/openalpr/runtime_data

### Uninstall

Remove tesseract:

```sh
sudo apt-get remove tesseract-ocr
```

Remove openalpr:

```sh
sudo apt-get autoremove openalpr
sudo apt-get autoremove libopenalpr

```
