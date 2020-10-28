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

perbedaan lainya adalah ketika kita memiliki nilai/state yang nantinya berubah-ubah maka gunakan statefull untul merender kembali nilai/state pada komponent sedangkan stateles untuk komponen yang nilainya/statenya tidak berubah

* Product.jsx
```javascript
import React, { Component, Fragment } from 'react';

class Product extends Component {
	state = {
		order: 4,
	}

	handlePlus = () => {
		this.setState({
			order: this.state.order + 1 //panggil state order sebelumnya ditambah 1
		})
	}

	handleMinus = () => {
		if (this.state.order > 0) {
			this.setState({
				order: this.state.order - 1 //panggil state order sebelumnya dikurangi 1
			})
		}
	}

	render() {
		return (
			<div className="container mb-5">
				<div className="card">
					<div className="card-header"> Header
					<div className="row">
							<div className="col-md-">
								<svg width="1em" height="1em" viewBox="0 0 16 16" className="ml-2 bi bi-cart-fill" fill="currentColor" xmlns="http://www.w3.org/2000/svg">
									<path fill-rule="evenodd" d="M0 1.5A.5.5 0 0 1 .5 1H2a.5.5 0 0 1 .485.379L2.89 3H14.5a.5.5 0 0 1 .491.592l-1.5 8A.5.5 0 0 1 13 12H4a.5.5 0 0 1-.491-.408L2.01 3.607 1.61 2H.5a.5.5 0 0 1-.5-.5zM5 12a2 2 0 1 0 0 4 2 2 0 0 0 0-4zm7 0a2 2 0 1 0 0 4 2 2 0 0 0 0-4zm-7 1a1 1 0 1 0 0 2 1 1 0 0 0 0-2zm7 0a1 1 0 1 0 0 2 1 1 0 0 0 0-2z" />
								</svg>
							</div>
							<div className="col-md">
                              {/*panggil state order*/}
								<div className="count">{this.state.order}</div>
							</div>
						</div>
					</div>
					<img src="" alt="" className="card-img-top" />
					<div className="card-body">
						<h5 className="card-title">Ayam Goreng</h5>
						<p className="card-text">Rp. 15000</p>
						<div className="input-group">
							<div className="input-group-append">
                            {/*panggil fungsi handleMinus*/}
								<button className="btn btn-warning minus" onClick={this.handleMinus}>-</button>
							</div>
                               {/*panggil state order*/}
							<input type="text" name="" id="" className="form-control text-center" value={this.state.order} />
							<div className="input-group-append">
                               {/*panggil fungsi handePlus*/}
								<button className="btn btn-primary plus" onClick={this.handlePlus}>+</button>
							</div>
						</div>
					</div>
				</div>
			</div>
		)
	}
}

export default Product;
```
membuat component product dan fungsi untuk menghandle perubahan data jumlah maupun kurang


* Home.jsx
import React, { Component } from 'react';
import YoutubeComponent from '../../component/YoutubeComponent/YoutubeComponent';
```javascript
import Product from '../Product/Product';

class Home extends Component {
    render() {
        return (
            <div>
                <Product></Product>
            </div>
        )
    }
}

export default Home;
```

lalu komponen tadi di panggil di home.js 

* Index.js
```javascript

import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import 'bootstrap/dist/css/bootstrap.min.css'
import App from './App';
import * as serviceWorker from './serviceWorker';
import Home from './container/Home/Home';

ReactDOM.render(<Home />, document.getElementById('root'));


// If you want your app to work offline and load faster, you can change
// unregister() to register() below. Note this comes with some pitfalls.
// Learn more about service workers: https://bit.ly/CRA-PWA
serviceWorker.unregister();
```

lalu di panggil home.js ke index.js agar bisa tampil pada browser

### Update Parent Component oleh Child Component ###
