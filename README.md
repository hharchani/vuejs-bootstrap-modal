# vuejs-bootstrap-modal

## Usage

import Bootstrap.css
``` html
<link href="/path/to/bootstrap.css"></link>
```

Simple options:
``` html
<!--text content-->
<modal title="Modal Title" v-modal="show" @ok="ok" @cancel="cancel">
    Modal Content
</modal>

<!--custom content-->
<modal v-modal="show" @ok="ok" @cancel="cancel">
    <div>Modal Body</div>

    <div slot="header">Modal Header</div>
    <div slot="footer">Modal Footer</div>
</modal>

```

## Props
``` javascript
props: {
    value: {
        type: Boolean,
        'default': false,
    },
    title: {
        type: String,
        'default': ''
    },
    small: {
        type: Boolean,
        'default': false
    },
    large: {
        type: Boolean,
        'default': false
    },
    closeByBackdrop: {
        type: Boolean,
        'default': true
    },
    showCloseButton: {
        type: Boolean,
        'default': true,
    },
    showCancelButton: {
        type: Boolean,
        'default': true,
    },
    okText: {
        type: String,
        'default': 'OK'
    },
    cancelText: {
        type: String,
        'default': 'Cancel'
    },
    okClass: {
        type: String,
        'default': 'btn btn-success'
    },
    cancelClass: {
        type: String,
        'default': 'btn btn-danger'
    },
    closeWhenOk: {
        type: Boolean,
        'default': false
    },
    showHeader: {
        type: Boolean,
        'default': true,
    },
    showFooter: {
        type: Boolean,
        'default': true,
    },
}
```

## Events

 - `shown` On finishing the entrance animation
 - `hidden` On finishing exit animation
 - `ok` On ok button press
 - `cancel` On cancel button press


# License
MIT

# Inspired by
[https://github.com/Coffcer/vue-bootstrap-modal](https://github.com/Coffcer/vue-bootstrap-modal)
