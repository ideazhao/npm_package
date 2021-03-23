# vue_tag_create

> vue project tags create

## Build Setup

``` bash
# install 
npm install vue_tag_create -S

# use
import vue-tag-create from "vue_tag_create"

# attributes

## layout (width error-tips)

- default:block
- inline: inline == true

## words limit

- default:none
- you can set it like `limit='15'`

## special characters check
- default:true

## trigger key
you can choose `enter` ,it is possible support `space` later. 

# events

## keyup 

trigger when keyup

## demo

<vue-tag-create 
  :limit='20' 
  :iconClass="iconClass" 
  :inline="true" 
  :placeholder="placeholder">
</vue-tag-create>

```

