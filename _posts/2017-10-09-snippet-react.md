---
layout: post
title: "Code: React template"
excerpt: "IntelliJ live template 용도"
categories: [code]
comments: false
---

```
import React, { Component, PropTypes } from 'react';

const propTypes = {

};

const defaultProps = {

};

class $MyComponent$ extends Component {
    
    constructor(props) {
        super(props);

    }

    render() {
        return (
            <div> 
                $Cursor$
            </div>
        );
    }
}

$MyComponent$.propTypes = propTypes;
$MyComponent$.defaultProps = defaultProps;

export default $MyComponent$;
```

