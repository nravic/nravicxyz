---
title: "Generative Art with Quil and Processing"
date: 2018-10-13T09:59:31+04:00
draft: true
---

I recently read an [article](https://www.artnome.com/news/2018/8/8/why-love-generative-art) on generative art. The space is incredible, and using controlled randomness to generate art seems like an amazing idea. I started looking at [Georg Nees'](https://www.wikiwand.com/en/Georg_Nees), and found my way to [Processing](https://processing.org). The gut instinct is always to look for a Python implementation, but I was unhappy with unweildly most were. I found [Quil](https://github.com/quil/quil) by chance, and fell in love. 

Quil weilds the Processing API in one hand, and Clojure in the other, using some fantastic language abstractions to make generating art a breeeze. I grokked it fairly easily, which resulted in the following pieces; which are simply a few concentric circles (the radii and colors of which follow gaussian distributions). 

![](/img/gen_art/1.jpg)
![](/img/gen_art/2.jpg)
![](/img/gen_art/3.jpg)

Clojure code: 
```clojure
(ns gen_art.dynamic
  (:require [quil.core :refer :all])
  (:require [incanter.core :as math])
  (:use [incanter.core :only [$=]])
  (:use [clojure.math.combinatorics :only [combinations cartesian-product]])
  (:use [clojure.pprint])
  (:use [clojure.set :only [union]])
  (:use [clojure.contrib.map-utils :only [deep-merge-with]])
  (:import [org.apache.commons.math3.distribution ParetoDistribution])
  (:import [processing.core PShape PGraphics]))

(defn setup []
  (frame-rate 10))      

(defn draw []
  (color-mode :hsb 360 100 100 1.0)
  (background 0 0 90)

  (def x 500)
  (def y 500)
  (def min-ellipse-rad 150)

  (defn gauss [mean variance]
  (+ mean (* variance (random-gaussian))))

  (doseq [i (range 20)]
    (let [actual-rad (+ min-ellipse-rad (gauss 0 100))]
      (fill (gauss 0 50) (gauss 50 100) (gauss 50 100) 0.3)
      (ellipse 250 250 actual-rad actual-rad)))

  (doseq [i (range 20)]
    (let [actual-rad (+ min-ellipse-rad (gauss 0 100))]
      (fill (gauss 50 100) (gauss 50 100) (gauss 50 100) 0.3)
      (ellipse 750 750 actual-rad actual-rad)))

  (doseq [i (range 20)]
    (let [actual-rad (+ min-ellipse-rad (gauss 0 100))]
      (fill (gauss 100 150) (gauss 50 100) (gauss 50 100) 0.3)
      (ellipse 250 750 actual-rad actual-rad)))

  (doseq [i (range 20)]
    (let [actual-rad (+ min-ellipse-rad (gauss 0 100))]
      (fill (gauss 150 360) (gauss 50 100) (gauss 50 100) 0.3)
      (ellipse 750 250 actual-rad actual-rad)))

  (save "sketch.tif"))
```

The above code only does the actual drawing. The actual code is best implemented in whatever Quil workflow you setup, mine follows [Tyler Hobbs'](http://www.tylerlhobbs.com/writings/using-quil-for-artwork) very closely. I'm excited to see what else Quil can do. I'm pretty sure ugly concentric circles are the least of it. 
