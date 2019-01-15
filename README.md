# $.ResponsiveScopes.js

### ResponsiveScopes is a jQuery based designer tool to synchronize and control reponsive layout changes

ResponsiveScopes defines scopes with label, min and max properties. It's events are triggered by the window resize event. The inbuilt "inertia" function fires only after the window resizing action has been ended. You can fine tune this behaviour with the "inertia" property.

Min breakpoints are used to calculate the scopes.
ResponsiveScopes can infix a label in a responsive url.
Callbacks can be attached to the following events: 


- **changed** (triggered at any scope change)
- **up**  (triggered at change to higher scope)
- **down** (triggered at change to lower scope)
- **formated** (triggered at format change. For instance "portrait" to "landscape").


```

// First argument: array of "min" breakpoints in entry or object format
// Second argument: options object or instance id

var breakpoints = { sm: 0, md: 768, lg: 1280 };

var rs = $.ResponsiveScopes( breakpoints, "rs1" );

rs.changed( handleScopeChange );

rs.formated( handleFormatChange );

```

### Event object properties

- **event**
- **instance**
- **id**
- **label**
- **index**
- **previousIndex**
- **change**
- **min**
- **max**
- **value**
- **format**
- **previousFormat**
- **ratio**


Callback

```

function handleScopeChange ( e ) {
    
    var rs = e.instance;
    
    // Update responsive image source
    // Example former "images/respImg_sm.png"
    // Example later "images/respImg_lg.png"
    
    img.src = rs.infix( img.src );
    
    if ( e.change > 0 && e.index === 2 ) {
        doBigChangeThings();
    }
    
    // ...
}

function  handleFormatChange ( e ) {
    
    if ( e.format === "portrait" ) {
        doPortraitLayoutThings();
    }
    else if ( e.ratio > 1.6 ) {
        doBroadStageStuff();
    }
    
    // ...
}

```

### Instance properties

- **previousIndex**:  number / getter
- **index**:  number / getter
- **change**:  number / getter
- **min**:  number / getter
- **max**:  number / getter
- **value**:  number / getter
- **format**: string / getter
- **ratio**: number / getter
- **scopes**:  array / getter
- **lable**:  string / getter
- **separator**:  string / getter-setter
- **inertia**:  number / getter-setter
- **autoUpdate**:  boolean / getter-setter
- **callbacks**:  boolean / getter-setter
- **hasCallbacks**:  boolean / getter

### Instance methods

- **update()**
- **define( obj_or_array )**
- **on( type, callbacks )**
- **off( type, callbacks )**
- **changed( callbacks )**
- **up( callbacks )**
- **down( callbacks )**
- **formated( callbacks )**
- **infix( url )**
- **unfix( url )**

**Tip:** Synchronize ResponsiveScopes with css min / max breakpoints