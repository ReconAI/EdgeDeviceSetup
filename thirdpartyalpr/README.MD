# Thrid-Party ALPR Libraries installation fuides

## OpenALPR
[Site](https://github.com/openalpr/openalpr)

### Prerequisites

```sh
sudo apt install tesseract-ocr
sudo apt install libtesseract-dev
```

### 1. Install using 'The Easy Way' !!! [Link](https://github.com/openalpr/openalpr/wiki/Compilation-instructions-(Ubuntu-Linux))

[Helpful instaruction](https://github.com/openalpr/openalpr/issues/660)

Next:
# Install the binaries/libraries to your local system (prefix is /usr)
sudo make install

# Test the library
wget http://plates.openalpr.com/h786poj.jpg -O lp.jpg
alpr lp.jpg


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



