---
layout: slide
title: React Accessibility Patterns
description: Solving specific a11y issues.
theme: present
highlight: tomorrow
transition: fade
---

<section class="main">
<img src="/css/images/2017-08-15-react-accessibility-patterns/QLogo.png" alt="Log of QDelft" style="max-width: 20%"/>
<h1>React Accessibility Patterns</h1>
<hr>
<ul>
    <li>Almero Steyn</li>
    <li>QDelft B.V.</li>
    <li>almerosteyn.com</li>
    <li>twitter.com/kryptos_rsa</li>
</ul>
</section>
<section>
<h1>React</h1>
<img src="/css/images/2017-08-15-react-accessibility-patterns/react-logo.svg" alt="React logo" style="max-width: 20%"/>
<blockquote>
"A JavaScript library for building user interfaces." - React docs
</blockquote>
</section>
<section>
<h1>Who uses React?</h1>
<img src="/css/images/2017-08-15-react-accessibility-patterns/facebook.png" alt="Facebook logo" style="max-width: 20%"/>
<img src="/css/images/2017-08-15-react-accessibility-patterns/Netflix.jpg" alt="Netflix logo" style="max-width: 20%"/>
<img src="/css/images/2017-08-15-react-accessibility-patterns/airbnb.png" alt="Airbnb logo" style="max-width: 20%"/>
<img src="/css/images/2017-08-15-react-accessibility-patterns/instagram.jpg" alt="Instagram logo" style="max-width: 20%"/>
<img src="/css/images/2017-08-15-react-accessibility-patterns/whatsapp.png" alt="Whatsapp logo" style="max-width: 20%"/>
<img src="/css/images/2017-08-15-react-accessibility-patterns/tenon.png" alt="Tenon logo" style="max-width: 20%"/>
<img src="/css/images/2017-08-15-react-accessibility-patterns/wehkamp.jpg" alt="Wehkamp logo" style="max-width: 20%"/>
<img src="/css/images/2017-08-15-react-accessibility-patterns/bbc.png" alt="BBC logo" style="max-width: 20%"/>
</section>
<section>
<h1>How accessible are they?</h1>
<img src="/css/images/2017-08-15-react-accessibility-patterns/goodbadugly.jpg" alt="Movie poster of The Good, the Bad and the Ugly"/>
</section>
<section>
<h1>The Good-a11y</h1>
<img src="/css/images/2017-08-15-react-accessibility-patterns/good.png" alt="The Good from the movie the Good, the Bad and the Ugly"/>
</section>
<section>
<img class="nomax" src="/css/images/2017-08-15-react-accessibility-patterns/tenoncap.png" alt="Image capture and Axe scan of tenon.io"/>
</section>
<section>
<img class="nomax" src="/css/images/2017-08-15-react-accessibility-patterns/airbnbcap.png" alt="Image capture and Axe scan of airbnb"/>
</section>
<section>
<h1>The other two</h1>
<img src="/css/images/2017-08-15-react-accessibility-patterns/bad.png" alt="The Good from the movie the Good, the Bad and the Ugly"/>
<img src="/css/images/2017-08-15-react-accessibility-patterns/ugly.png" alt="The Good from the movie the Good, the Bad and the Ugly"/>
</section>
<section>
<img class="nomax" src="/css/images/2017-08-15-react-accessibility-patterns/wehkampcap.png" alt="Image capture and Axe scan of wehkamp"/>
</section>
<section>
<img class="nomax" src="/css/images/2017-08-15-react-accessibility-patterns/dockercap.png" alt="Image capture and Axe scan of docker"/>
</section>
<section>
<h1>But why?</h1>
<img src="/css/images/2017-08-15-react-accessibility-patterns/grumpy-confused-cat.png" alt="Cat confused about the accessible state of React websites"/>
</section>
<section>
<img src="/css/images/2017-08-15-react-accessibility-patterns/divtobutton.jpg" alt="Image of Harry Potter turning a div into a button"/>
    <pre><code class="html" data-trim>
        <div className="looks-like-a-button"
             onClick={this.onClickHandler}>
               Press me please
        </div>
    </code></pre>
</section>
<section>
<h1>There has to be a better way?</h1>
<img src="/css/images/2017-08-15-react-accessibility-patterns/confused.jpg" alt="Confusion about how bad the web is"/>
</section>

<section>
<h1>Example application</h1>
<a href="https://github.com/AlmeroSteyn/react-a11y-patterns">https://github.com/AlmeroSteyn/react-a11y-patterns</a>
</section>
<section>
<h1>React component tree</h1>
<img src="/css/images/2017-08-15-react-accessibility-patterns/react-components.png" alt="Depicts the React virtual DOM and how it relates to the real DOM"/>
</section>
<section>
<h1>React component class</h1>
<pre><code class="javascript" data-trim>
import React, { Component } from 'react';

class Demo extends Component {
    render() {
        return (
            <span>{this.props.displayText}</span>
        );
    }
}

export default Demo;

</code></pre>
</section>
<section>
<h1>React component function</h1>
<pre><code class="javascript" data-trim>
import React from 'react';

const Demo = ({ displayText }) => (
    <span>{displayText}</span>
);

export default Demo;
</code></pre>
</section>
<section>
<h1>Using a component</h1>
<pre><code class="javascript" data-trim>
import React from 'react';
import Demo from './Demo';

const Root = () => (
     &lt;Demo displayText="Show this text"/>
);

export default Root;
</code></pre>
</section>
<section>
<h1>React virtual DOM + Reconciler</h1>
<img src="/css/images/2017-08-15-react-accessibility-patterns/reactdom.png" alt="Depicts the React virtual DOM and how it relates to the real DOM"/>
</section>
<section>
<h1>React virtual DOM in browser</h1>
<img class="nomax" src="/css/images/2017-08-15-react-accessibility-patterns/reactdominbrowser.png" alt="A debug view of the React DOM in React dev tools"/>
</section>
<section>
<h1>React actual DOM in browser</h1>
<img class="nomax"  src="/css/images/2017-08-15-react-accessibility-patterns/realdominbrowser.png" alt="A debug view of the DOM to compare to that of the React DOM of the previous slide"/>
</section>
<section>
    <h1>JSX</h1>
    <p>HTML-like syntactic JavaScript sugar.</p>
    <pre><code class="html" data-trim>
        <label htmlFor={nameId}>{nameLabelText}</label>
        <input id={nameId} type="text" />
    </code></pre>
    Renders to HTML in the DOM.
    <pre><code class="html" data-trim>
         <label for="name">Darth Vader</label>
         <input id="name" type="text" />
    </code></pre>
</section>
<section>
<h1>Good HTML makes good JSX</h1>
<pre><code class="html" data-trim>
const AppNavigation = () =>
  <aside>
    <nav>
      <ul className="nav nav-pills nav-stacked">
        <li>
          <NavLink
            to={pathname}
            activeClassName="active">
            Contact
          </NavLink>
        </li>
      </ul>
    </nav>
  </aside>;
</code></pre>
</section>
<section>
<h1>First rule of ARIA</h1>
    <p>Bad idea:</p>
     <pre><code class="html" data-trim>
       <div className="looks-like-button"
            onClick={this.onClickHandler}>
         Press me
       </div>
     </code></pre>
    <p>Good idea:</p>
     <pre><code class="html" data-trim>
         <button onClick={this.onClickHandler}>
            Press
         </button>
     </code></pre>
</section>
<section>
<h1>Intact header symantics</h1>
<img class="nomax" src="/css/images/2017-08-15-react-accessibility-patterns/headers.png" alt="Diagram of HTML headers"/>
<pre><code class="html" data-trim>
const HeaderWithLevel = ({ headerText, level }) => {
  const HeaderLevel = `h${level}`;
  return &lt;HeaderLevel>{headerText}&lt;/HeaderLevel>;
};
</code></pre>
</section>
<section>
<h1>Components and unique id's</h1>
 <pre><code class="html" data-trim>
 import uuid from 'uuid';
 //...
 this.inputId = uuid.v4();
 //...
 render() {
    //...
    <label htmlFor={this.inputId}>
      {labelText}
    </label>
    <input id={this.inputId}
      onChange={this.onChangeHandler}
      value={value}
    />
    //...
 }
 </code></pre>
 <a href="https://github.com/kelektiv/node-uuid">https://github.com/kelektiv/node-uuid</a>
</section>
<section>
<h1>Routing is a11y silent</h1>
<pre><code class="html" data-trim>
const AppMain = () =>
  <main>
    &lt;Switch>
      <Route path="/todos" component={Todos} />
      <Route path="/todo" component={Todo} />
      <Route path="/contact" component={Contact} />
      &lt;Redirect to="/todos" />
    &lt;/Switch>
  </main>;
</code></pre>
</section>
<section>
<h1>Set focus after navigation</h1>
<pre><code class="html" data-trim>
class PageFocusSection extends Component {
  componentDidMount() {
    this.header.focus();
  }
  render() {
    const { children, headingText } = this.props;
    return (&lt;section>
        <h2 tabIndex="-1" ref={header => (this.header = header)}>
          {headingText}
        </h2>
        {children}
      &lt;/section>);
  }
}
</code></pre>
</section>
<section>
<h1>Changing the document title</h1>
<pre><code class="html" data-trim>
//...
import DocumentTitle from 'react-document-title';
//...
const SetDocTitle = ({ docTitle, children }) =>
  <DocumentTitle title={docTitle}>
    {children}
  </DocumentTitle>;
</code></pre>
<a href="https://github.com/gaearon/react-document-title">https://github.com/gaearon/react-document-title</a>
</section>
<section>
<h1>ARIA live announcer</h1>
<pre><code class="html" data-trim>
//...
import { LiveAnnouncer, LiveMessage } from 'react-aria-live';
//...
render() {
return (
  &lt;LiveAnnouncer>
    &lt;LiveMessage message={this.state.a11yMessage}
                 aria-live="polite" />
    {this.props.children}
  &lt;/LiveAnnouncer>
);
}
//..
</code></pre>
<a href="https://github.com/AlmeroSteyn/react-aria-live">https://github.com/AlmeroSteyn/react-aria-live</a>
</section>
<section>
 <video controls class="stretch" src="/css/videos/2017-08-15-react-accessibility-patterns/a11yappwalkthrough.mp4" type="video/mp4">
        Your browser does not support the video tag.
</video>
</section>
<section>
<h1>React a11y docs</h1>
<img class="nomax" src="/css/images/2017-08-15-react-accessibility-patterns/reactdocs.png" alt="Screenshot of the React accessibility docs"/>
</section>
<section class="main">
<h1>Questions</h1>
<hr>
<p>Presentation online at:</p>
<a href="http://almerosteyn.com/slides/">http://almerosteyn.com/slides/</a>
<hr>
<ul>
    <li>Almero Steyn</li>
    <li>QDelft B.V.</li>
    <li>almerosteyn.com</li>
    <li>twitter.com/kryptos_rsa</li>
</ul>
</section>
