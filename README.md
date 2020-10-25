# catatan-react
### Statefull dan Stateless ###

* Penulisan Stateless
stateless component sama dengan functional component
```javascript
import React from 'react';

// cara import css
import './HelloComponent.css';


const HelloComponent = () => {
    return <p className="text-p"> Hello Functional Component </p>
}

export default HelloComponent;
```

* Penulisan Statefull
```javascript
import React from 'react';

class StateFullComponent extends React.Component {
    render() {
        return <p>Hello StateFull Component</p>
    }
}

export default StateFullComponent;
```

*
