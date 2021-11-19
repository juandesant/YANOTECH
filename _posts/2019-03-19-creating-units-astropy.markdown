---
author: Juande Santander-Vela
title: "Creating units in AstroPy"
date:   2019-03-19 13:22:30 -0300
category: [astropy, python]
tags: python astropy units conversion currency
---

I am writing this post as a reminder to myself of how to create units in AstroPy.

The first enchantment to use units in AstroPy is to type (remeber that `>>> ` represents the Python prompt, and must not be typed):

    >>> from astropy import units as u

This allows you to just use `u.` as a prefix to your units, and to things like

    >>> (u.km/u.h).to(u.m/u.s)

to convert between between kilometres per hour and metres per second, or the more astronomically oriented:

    >>> (u.lightyear).to(u.m)
    9460730472580800.0

But many times you want to do calculations that involve currencies mixed with other units, and there is —understandably— no support for those in AstroPy.

It does not matter: you can create your own units in AstroPy!

<!--more-->
## The problem with AstroPy documentation
Unfortunately, it is not very easy to find the documentation for how to create units in AstroPy: if you type

    >>> help(u.Unit)

you get something like this:

    Help on class Unit in module astropy.units.core:
    
    class Unit(NamedUnit)
     |  Unit(s, represents=None, format=None, namespace=None, doc=None, parse_strict='raise')
     |  
     |  The main unit class.
     |  
     |  There are a number of different ways to construct a Unit, but
     |  always returns a `UnitBase` instance.  If the arguments refer to
     |  an already-existing unit, that existing unit instance is returned,
     |  rather than a new one.
     |  
     |  - From a string::
     |  
     |      Unit(s, format=None, parse_strict='silent')
     |  
     |    Construct from a string representing a (possibly compound) unit.
     |  
     |    The optional `format` keyword argument specifies the format the
     |    string is in, by default ``"generic"``.  For a description of
     |    the available formats, see `astropy.units.format`.
     |  
     |    The optional ``parse_strict`` keyword controls what happens when an
     |    unrecognized unit string is passed in.  It may be one of the following:
     |  
     |       - ``'raise'``: (default) raise a ValueError exception.
     |  
     |       - ``'warn'``: emit a Warning, and return an
     |         `UnrecognizedUnit` instance.
     |  
     |       - ``'silent'``: return an `UnrecognizedUnit` instance.
     |  
     |  - From a number::
     |  
     |      Unit(number)
     |  
     |    Creates a dimensionless unit.
     |  
     |  - From a `UnitBase` instance::
     |  
     |      Unit(unit)
     |  
     |    Returns the given unit unchanged.
     |  
     |  - From `None`::
     |  
     |      Unit()
     |  
     |    Returns the null unit.
     |  
     |  - The last form, which creates a new `Unit` is described in detail
     |    below.

The last phrase is tantalising: it promises you that you can create a new unit based on an empty definition!

However, if you type:

    >>> u.Unit()

you will be greeted by an error: `TypeError: __call__() missing 1 required positional argument: 's'`

You can try instead:

    >>> u.Unit("")

which successfuly returns a dimensionless unit… that has no name, and to which you cannot attach any conversions!

## The solution: use `u.def_unit()`

If you search through AstroPy documentation —i.e., by searching [`site:astropy.org define new unit`][duck_astropy_unit]—, you will find the AstroPy documentation page for creating new units, aptly named [Combining and Defining Units][combine_define_units].

With that required reading finished, I can now define a unit for the Euro as:

    >>> EUR=u.def_unit(["EUR", "€", "euro", "euros", "eur"])

I can later define a unit for the US Dolar, with an equivalency to the Euro (as of March 19, 2019):

    >>> USD=u.def_unit(["USD", "$", "dolar", "dolars", "US dolar"], 1000./882.20*EUR)

In this way, you can convert USD to EUR and viceversa:

    >>> (500*USD).to(EUR)
    <Quantity 566.76490592 EUR>
    
    >>> (500*EUR).to(USD)
    <Quantity 441.1 USD>

## Using other units with your own: storage price calculations
And why am I working with currencies? I'm looking at storage prices across different cloud providers, and being able to attach a price per gigabyte per month, and then calculate the price for a full petabyte for a year is quite useful.

For instance, assuming a price of 0.05 USD per gigabyte per month, the price of storing a petabyte for a year can be easily calculated now as:

    >>> storage_cost = 0.05*USD/u.gigabyte/(30*u.day)
    >>> storage_cost*u.petabyte*u.year
    <Quantity 0.00166667 Pbyte USD yr / (d Gbyte)>

So, if you want to normalise it, you need to calculate it as:

    >>> (storage_cost*u.petabyte*u.year).to(USD)
    <Quantity 608750. USD>

or

    >>> (storage_cost*u.petabyte*u.year).decompose()
    <Quantity 608750. USD>

You could, instead, just get the factor in USD per petabyte per year:

    >>> storage_cost.to(USD/u.petabyte/u.year)
    <Quantity 608750. USD / (Pbyte yr)>

I hope that helps! It will sure help me remember how to do this the next time ;-)

[duck_astropy_unit]: http://duckduckgo.com/?q=site:astropy.org+define+new+unit "Search in DuckDuckGo for 'define new unit' within astropy.org"
[combine_define_units]: http://docs.astropy.org/en/stable/units/combining_and_defining.html "AstroPy Docs: Combining and Defining Units"
