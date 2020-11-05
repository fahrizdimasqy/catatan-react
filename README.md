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
```javascript
import React, { Component } from 'react';
import YoutubeComponent from '../../component/YoutubeComponent/YoutubeComponent';
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
* Product.jsx
```javascript
import React, { Component, Fragment } from 'react';
import CardProduct from '../CardProduct/CardProduct';

class Product extends Component {
	state = {
		order: 4,
	}

	// fungsi untuk mengupadte state order
	handleCounterChange = (newValue) => {
		this.setState({
			order: newValue //new value disini mengirimkan nilai dari cardProduct ke )roduct melalui newValue, newValue adalah value yang diterima dari komponen CardProduct 
		})
	}

	render() {
		return (
			<Fragment>
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
									<div className="count">{this.state.order}</div>
								</div>
							</div>
						</div>
						<img src="" alt="" className="card-img-top" />

						{/* memanggil child komponent yang cardProduct */}
						{/* onCounterChange adalah props */}
						<CardProduct onCounterChange={(value) => this.handleCounterChange(value)} /> {/* memanggil fungsi this.handleCounter untuk mengirimkan value*/}
						{/* {(value)} adalah nilai yang dierima dari function handleCounterChange yang memanggil onCounterChange pada CardProduct dan value itu dikirimkan ke handleCounterChange di Product ini dan this.handleCounterChange(value) value itu dikirmkan ke method handleCounterChange di komponen Product yang namanya diubah menjadi newValue*/}

					</div>
				</div>
			</Fragment>
		)
	}
}

export default Product;
```
* CardProduct.jsx
```javascript
import React, { Component, Fragment } from 'react';

class CardProduct extends Component {
    state = {
        order: 4,
    }

    // fungsi/method ketika counter berubah akan meng execute props di Componen CardProduct yang di panggil di Product
    handleCounterChange = (newValue) => {
        this.props.onCounterChange(newValue) //memanggil props di componen CardProduct yang di panggil di Product
        // sehingga onCounterChange disini akan menerima data dari handlePlus dan datanya akan dikirimkan ke props di komponent CardProduct yang di panggil Product

        // dan new value itu yang akan mengupdate order di Product

        // kemudian ditangkap di method disini
    }

    // ketika plus di execute maka panggil method handleCounterChange
    handlePlus = () => {
        this.setState({
            order: this.state.order + 1
        }, () => { this.handleCounterChange(this.state.order) }) //handleCounterChange akan mengirimi value state terbaru
        this.handleCounterChange();
    }

    handleMinus = () => {
        if (this.state.order > 0) {
            this.setState({
                order: this.state.order - 1
            }, () => { this.handleCounterChange(this.state.order) })
            this.handleCounterChange()
        } else {
            alert('tidak bisa minus');
        }
    }

    render() {
        return (
            <div className="card-body">
                <h5 className="card-title">Ayam Goreng</h5>
                <p className="card-text">Rp. 15000</p>
                <div className="input-group">
                    <div className="input-group-append">
                        <button className="btn btn-warning minus" onClick={this.handleMinus}>-</button>
                    </div>
                    <input type="text" name="" id="" className="form-control text-center" value={this.state.order} />
                    <div className="input-group-append">
                        <button className="btn btn-primary plus" onClick={this.handlePlus}>+</button>
                    </div>
                </div>
            </div>
        )
    }
}

export default CardProduct;
```

* Home.jsx
```javascript
import React, { Component } from 'react';
import YoutubeComponent from '../../component/YoutubeComponent/YoutubeComponent';
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
* Index.jsx
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
### LifeCycle Component
### 1. Mounting ###
Ketika komponent itu dipasang
Mounting > Constructor > getDerivedFromprops > componentDidMount
### 2. Updating ###
Ketika Komponent itu update
### 3. UnMounting ###
Ketika komponen itu dicopot atau dihilang di page kita

* LifeCycleComp.jsx
```javascript
import React, { Component } from 'react';

class LifeCycleComp extends Component {
    constructor(props) {
        super(props);
        this.state = {
            count: 1
        }
        console.log('constructor')
    }

    static getDerivedStateFromProps(props, state) {
        console.log('komponen getDerivedStateFromProps')
        return null;
    }

    componentDidMount() {
        console.log('componentDidMount')
        // untuk mengupdate state
        setTimeout(() => {
            this.setState({
                count: 2
            })
        }, 3000)
    }

    shouldComponentUpdate(nextProps, nextState) {
        console.log('shouldComponentUpdate')
        return true; // ketika state di update maka function ini harus di return true
    }

    getSnapshotBeforeUpdate(prevProps, prevState) {
        console.log('getSnapshotBeforeUpdate')
    }

    componentDidUpdate(prevProps, prevState, snapshot) {
        console.log('komponenDidUpdate')
    }

    componentWillUnmount() {
        console.log('componentWillUnmount')
    }

    render() {
        console.log('render')
        return (
            <button className="btn btn-primary ml-2">Component Button {this.state.count}</button>
        );
    }
}

export default LifeCycleComp;
//hasilnya 2
```

* Home.jsx
```javascript
import React, { Component } from 'react';
import YoutubeComponent from '../../component/YoutubeComponent/YoutubeComponent';
import LifeCycleComp from '../LifeCycleComp/LifeCycleComp';
import Product from '../Product/Product';

class Home extends Component {
    render() {
        return (
            <div>
                {/* <Product></Product> */}
                <LifeCycleComp />
            </div>
        )
    }
}

export default Home;
```

### LifeCycle part 2 ###
* LifeCylceComp.jsx
```javascript
import React, { Component } from 'react';

class LifeCycleComp extends Component {
    constructor(props) { // contructor akan di tampilkan pertama
        super(props);
        this.state = {
            count: 1 // yang pertama tampil di page
        }
        console.log('constructor')
    }

    static getDerivedStateFromProps(props, state) { // life cycle kedua yang ditampilkan
        console.log('komponen getDerivedStateFromProps')
        return null;
    }

    componentDidMount() {
        console.log('componentDidMount')
        // untuk mengupdate state
        setTimeout(() => {
            this.setState({
                count: 2
            })
        }, 5000)
    }

    shouldComponentUpdate(nextProps, nextState) {
        console.log('shouldComponentUpdate')
        return true;
    }

    getSnapshotBeforeUpdate(prevProps, prevState) {
        console.log('getSnapshotBeforeUpdate')
        return null;
    }

    componentDidUpdate(prevProps, prevState, snapshot) {
        console.log('komponenDidUpdate')
    }

    componentWillUnmount() {
        console.log('componentWillUnmount')
    }

    render() {
        console.log('render')
        return (
            <button className="btn btn-primary ml-2">Component Button {this.state.count}</button>
        );
    }
}

export default LifeCycleComp;
```

* Home.jsx
```javascript
import React, { Component } from 'react';
import YoutubeComponent from '../../component/YoutubeComponent/YoutubeComponent';
import LifeCycleComp from '../LifeCycleComp/LifeCycleComp';
import Product from '../Product/Product';

class Home extends Component {

    state = {
        showComponent: true
    }

    componentDidMount() {
        setTimeout(() => {
            this.setState({
                showComponent: false
            })
        }, 15000) // setelah 15 detik component ini akan dihilangkan
    }

    render() {
        return (
            <div>

                {
                    this.state.showComponent
                        ?
                        <LifeCycleComp />
                        : null
                }
            </div>

        )
    }
}

export default Home;
```
> hasil: dipanggil component constructor dengan nilai sebelumnya yaitu 1 lalu ditampilkan, lalu component componentDidMount diberi perintah untuk mengupdate state jadi 2 setelah dipasang dan mendapatkan nilai props/state sebelumnya yang di ubah melalu component componentDidMount, lalu shouldComponentUpdate menanyakan apakah ada nilai yang diubah jika ya return nilainya jadi true maka setelah 5 detik akan ditampilkan component dengan nilai yang telah diupdate lalu akan ditampilkan nilai yang telah di update kedalam page dan component, lalu mengexsekusu componentDidUpdate sudah di update, dan setelah 15 detik componen hilang componentWillUnmount

### studi kasus LifeCycle ###
* LifeCycleComp.jsx
```javascript
import React, { Component } from 'react';

class LifeCycleComp extends Component {
    constructor(props) { // contructor akan di tampilkan pertama
        super(props);
        this.state = {
            count: 1 // yang pertama tampil di page
        }
        console.log('constructor')
    }

    static getDerivedStateFromProps(props, state) { // life cycle kedua yang ditampilkan
        console.log('komponen getDerivedStateFromProps')
        return null;
    }

    componentDidMount() {
        console.log('componentDidMount')
        // // untuk mengupdate state
        // setTimeout(() => {
        //     this.setState({
        //         count: 2
        //     })
        // }, 5000)
    }
    // arti component ini adalah haruskan komponen ini harus diupdate
    // kalau tidak perlu dia akan memanggil lifeCycle lainya keluar dan selesai
    shouldComponentUpdate(nextProps, nextState) { // dua parameter ini bisa mencegah componen kita di update
        console.group('shouldComponentUpdate')
        // console.log('shouldComponentUpdate')
        // console.log(nextProps);
        console.log('next state', nextState);
        console.log('this state', this.state)
        console.groupEnd();
        if (nextState.count >= 4) { // ketika count bernilai 4/ lebih besar maka tidak akan d update
            return false
        }
        return true;
    }

    getSnapshotBeforeUpdate(prevProps, prevState) {
        console.log('getSnapshotBeforeUpdate')
        return null;
    }

    componentDidUpdate(prevProps, prevState, snapshot) {
        console.log('komponenDidUpdate')
    }

    componentWillUnmount() {
        console.log('componentWillUnmount')
    }

    // method ini akan menjalankan menambah countnya jadi nilai count sebelumnya ditambah count + 1
    changeCount = () => {
        this.setState({
            count: this.state.count + 1
        })
    }

    render() {
        console.log('render')
        return (
            <button className="btn btn-primary ml-2" onClick={this.changeCount}>Component Button {this.state.count}</button> //ketika buttonnya diklick maka buttin akan memanggil method yang telah dibuat dengan nama changeCount
        );
    }
}

export default LifeCycleComp;
```

* Home.jsx
```javascript
import React, { Component } from 'react';
import YoutubeComponent from '../../component/YoutubeComponent/YoutubeComponent';
import LifeCycleComp from '../LifeCycleComp/LifeCycleComp';
import Product from '../Product/Product';

class Home extends Component {

    state = {
        showComponent: true
    }

    componentDidMount() {
        // setTimeout(() => {
        //     this.setState({
        //         showComponent: false
        //     })
        // }, 15000) // setelah 15 detik component ini akan dihilangkan
    }

    render() {
        return (
            <div>

                {
                    this.state.showComponent
                        ?
                        <LifeCycleComp />
                        : null
                }
            </div>

        )
    }
}

export default Home;
```

> kesimpulan 1. mounting (pemasangan) didalam mounting ini kita memiliki beberapa lifecycle yaitu: (constructor,getDerivedStateFromProps,rende, componentDidMount) 2. updating memiliki lifecycle(getDerivedStateFromProps, shouldComponentUpdate, render, getSnapshotBeforeUpdate, componentDidUpdate) 3. unmounting(pecopotan komponent) memiliki lifecycle(componentWillUnmount)

### Berinteraksi dengan API menggunakan Fetch

* BlogPost.jsx
```javascript
import React, { Component, Fragment } from 'react';
import Post from '../../component/Post/Post';
class BlogPost extends Component {
    state = {
        post: []
    }

    // ketika component dipasang
    componentDidMount() {
        // mengambil data ke server
        fetch('https://jsonplaceholder.typicode.com/posts')
            .then(response => response.json()) //diubah menjadi json
            .then(json => {
                this.setState({
                    post: json //lalu objek state key post valuenya diganti menjadi data json yang didapat di server
                })
            })
    }

    render() {
        return (
            <Fragment>
                <div className="container">
                    <h4>Blog Post</h4>
                    <hr />
                    {
                        //melooping data state yang sudah memiliki data json
                        this.state.post.map(post => {
                            //lalu di return/mengembalikan nilai bersarkan key/name pada objek json
                            return <Post key={post.id} no={post.id} title={post.title} p desc={post.body} />
                        })
                    }
                </div>
            </Fragment>
        );
    }
}
export default BlogPost;
```

* Post.jsx
```javascript
import React, { Fragment } from 'react';
import './Post.css'
const Post = (props) => {
    return (
        <Fragment>
            <div className="card mb-3">
                <div className="row no-gutters">
                    <div className="col-md-4">
                        <img src="https://images3.alphacoders.com/221/thumb-1920-221297.png" alt="" className="card-img" />
                    </div>
                    <div className="col-md-8">
                        <div className="card-body">
                            {/* memanggil props yang berisi data json dengan name no dan ditampilkan */}
                            <p className="card-text">{props.no}</p>
                            {/* memanggil props yang berisi data pada json dengan name title dan ditampilkan */}
                            <h5 className="card-title">{props.title}</h5>
                            {/* memanggil props yang berisi data pada json dengan name desc dan ditampilkan */}
                            <p className="card-text">
                                {props.desc}
                            </p>
                        </div>
                    </div>
                </div>
            </div>
        </Fragment>
    )
}
export default Post;
```

* Home.jsx
```javascript
import React, { Component } from 'react';
import YoutubeComponent from '../../component/YoutubeComponent/YoutubeComponent';
import BlogPost from '../BlogPost/BlogPost';
import LifeCycleComp from '../LifeCycleComp/LifeCycleComp';
import Product from '../Product/Product';

class Home extends Component {
    render() {
        return (
            <div>
                <BlogPost />
            </div>

        )
    }
}

export default Home;
```
### Berinteraksi menggunakan axios
* BlogPost.jsx
```javascript
import React, { Component, Fragment } from 'react';
import Post from '../../component/Post/Post';
import axios from 'axios';

class BlogPost extends Component {
    state = {
        post: []
    }

    // ketika component dipasang
    componentDidMount() {
        // mengambil data ke server
        axios.get('https://jsonplaceholder.typicode.com/posts')
            .then((result) => {
                console.log(result.data) //mengambil data pada api
                this.setState({
                    post: result.data // mengubah post dengan data yang ada di api
                })
            })
    }

    render() {
        return (
            <Fragment>
                <div className="container">
                    <h4>Blog Post</h4>
                    <hr />
                    {
                        //melooping data state yang sudah memiliki data json
                        this.state.post.map(post => {
                            //lalu di return/mengembalikan nilai bersarkan key/name pada objek json
                            return <Post key={post.id} no={post.id} title={post.title} p desc={post.body} />
                        })
                    }
                </div>
            </Fragment>
        );
    }
}
export default BlogPost;
```

* Post.jsx
```javascript
import React, { Fragment } from 'react';
import './Post.css'
const Post = (props) => {
    return (
        <Fragment>
            <div className="card mb-3">
                <div className="row no-gutters">
                    <div className="col-md-4">
                        <img src="https://images3.alphacoders.com/221/thumb-1920-221297.png" alt="" className="card-img" />
                    </div>
                    <div className="col-md-8">
                        <div className="card-body">
                            {/* memanggil props yang berisi data json dengan name no dan ditampilkan */}
                            <p className="card-text">{props.no}</p>
                            {/* memanggil props yang berisi data pada json dengan name title dan ditampilkan */}
                            <h5 className="card-title">{props.title}</h5>
                            {/* memanggil props yang berisi data pada json dengan name desc dan ditampilkan */}
                            <p className="card-text">
                                {props.desc}
                            </p>
                        </div>
                    </div>
                </div>
            </div>
        </Fragment>
    )
}
export default Post;
```

* Home.jsx
```javascript
import React, { Component } from 'react';
import YoutubeComponent from '../../component/YoutubeComponent/YoutubeComponent';
import BlogPost from '../BlogPost/BlogPost';
import LifeCycleComp from '../LifeCycleComp/LifeCycleComp';
import Product from '../Product/Product';

class Home extends Component {
    render() {
        return (
            <div>
                <BlogPost />
            </div>

        )
    }
}

export default Home;
```
