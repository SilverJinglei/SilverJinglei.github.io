# C Resource
http://beej.us/guide/bgc/html/single/bgc.html#stclasses

# C lang Design Pattern

## Overview

c lang only have [struct] => simulate [class] in c++

c lang don’t has:

1. inheritance
2. template <T>
3. member function

## GOF

> GOF use class (type) and object (instance) => play Pattern
>
> Therefore, c-lang only use [instance] way is enough.(class is no way)

### Assembly Instance => Gen Instance

>  Strategy Use Instance to create instance

#### Build

#### Factory Method

#### Prototype (Clone)

# Interface

interface only consist of Methods (no any field) => struct + function pointer

## Factory Method

https://softwareengineering.stackexchange.com/questions/333576/what-does-the-following-definition-of-an-interface-mean

```c
#include<stdio.h>

// 1. define Interface
typedef struct {
    /// Prints a key-value pair, where value is an integer
    void (*printIntItem)(char key[], int value);
    /// Prints a key-value pair, where the value is a string
    void (*printStringItem)(char key[], char value[]);
} PrintInterface;

// 2. Factory => JsonImp
void json_printIntItem(char key[], int value) {
    printf("{\"%s\": %d}\n", key, value);
}
void json_printStringItem(char key[], char value[]) {
    printf("{\"%s\": \"%s\"}\n", key, value);
}
PrintInterface PrintJson() {
    PrintInterface interface;
    interface.printIntItem = json_printIntItem;
    interface.printStringItem = json_printStringItem;
    return interface;
}

// 3. Factory => StingImp
void xml_printIntItem(char key[], int value) {
    printf("<%s>%d</%s>\n", key, value, key);
}
void xml_printStringItem(char key[], char value[]) {
    printf("<%s>%s</%s>\n", key, value, key);
}
PrintInterface PrintXml() {
    PrintInterface interface;
    interface.printIntItem = xml_printIntItem;
    interface.printStringItem = xml_printStringItem;
    return interface;
}

// 4. Use Imp
void printStuff(PrintInterface implementation) {
    implementation.printIntItem("one", 1);
    implementation.printStringItem("two", "2");
}

int main() {
    PrintInterface jsonImpl = PrintJson();
    printStuff(jsonImpl);

    PrintInterface xmlImpl = PrintXml();
    printStuff(xmlImpl);
    return 0;
}
```

# Inheritance & Polymorphism

https://stackoverflow.com/questions/6304794/oop-and-interfaces-in-c

## Inheritance

Has a => (replace) is a

```c
typedef struct parent
{
    
}parent;

typedef struct child
{
    parent* base;
    child* this;
}child;


```

# Refactor

## Terminate Switch
Marcro dispatch switch case

```c
switch(enum)
{
    case e1:
    case e2:
    default:
}

=>

#define HandleEnum(x) x##_Func(x)

HandleEnum(enum);

```

## My Idea

Has a => (replace) is a

```c
typedef struct parent
{
    
}parent;

typedef struct child
{
    parent* base;
    child* this;
}child;
```
