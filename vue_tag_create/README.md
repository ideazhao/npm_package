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
- default:none
- you can use it by `charCheck = true`

## trigger key
you can choose `enter` or `space` you like 

# events

## input 

trigger when input

## blur

trigger when blur

## focus

trigger when focus

## demo

<vue-tag-create 
  :wordLimit='20' 
  :iconClass="iconClass" 
  :inline="true" 
  :placeholder="placeholder">
</vue-tag-create>

```

