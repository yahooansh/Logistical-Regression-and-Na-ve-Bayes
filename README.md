# Logistical-Regression-and-Na-ve-Bayes
Using the water_potability.csv to create a forecasting model using both Logistical Regression and Naïve Bayes.Dataset contains: 2,007 observations and 10 variables: 
Independent Variables 
ph -  acid–base balance of water 
Hardness - Hardness is mainly caused by calcium and magnesium salts.  
Solids -  Total dissolved solids - TDS  
Chloramines - Chlorine and chloramine are the major disinfectants used in public water systems 
Sulfate - naturally occurring substances that are found in minerals, soil, and rocks.  
Conductivity - pure water is not a good conductor of electric current rather’s a good insulator 
Organic_carbon - Total Organic Carbon (TOC)  
Trihalomethanes - THMs are chemicals which may be found in water treated with chlorine 
Turbidity - depends on the quantity of solid matter present in the suspended state.  

Dependent Variables 
Potability - 1 means Potable (Drinkable) and 0 means Not potable (Not Drinkable). 


![Screenshot 2024-10-26 143302](https://github.com/user-attachments/assets/d215ecc4-a10d-4ef2-90b4-fc947ebad7d0)
[Presentation.pptx](https://github.com/user-attachments/files/17531645/Presentation.pptx)
[Uploading Code.h<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd"><html><head></head><body>















    




    
    
    
    

<div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs">
<div class="jp-Cell-inputWrapper">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In&#160;[27]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor">
     <div class="CodeMirror cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="c1"># importing necessary libraries</span>
<span class="kn">import</span> <span class="nn">numpy</span> <span class="k">as</span> <span class="nn">np</span>
<span class="kn">import</span> <span class="nn">pandas</span> <span class="k">as</span> <span class="nn">pd</span>
<span class="kn">import</span> <span class="nn">matplotlib.pyplot</span> <span class="k">as</span> <span class="nn">plt</span>
<span class="o">%</span><span class="k">matplotlib</span> inline
<span class="kn">import</span> <span class="nn">seaborn</span> <span class="k">as</span> <span class="nn">sns</span>
</pre></div>

     </div>
</div>
</div>
</div>

</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In&#160;[28]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor">
     <div class="CodeMirror cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="c1">#load dataset</span>
<span class="n">dataset</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">read_csv</span><span class="p">(</span><span class="s1">&#39;./water_potability.csv&#39;</span><span class="p">)</span>
<span class="n">dataset</span><span class="o">.</span><span class="n">head</span><span class="p">()</span>
</pre></div>

     </div>
</div>
</div>
</div>

<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>


<div class="jp-OutputArea jp-Cell-outputArea">

<div class="jp-OutputArea-child">

    
    <div class="jp-OutputPrompt jp-OutputArea-prompt">Out[28]:</div>



<div class="jp-RenderedHTMLCommon jp-RenderedHTML jp-OutputArea-output jp-OutputArea-executeResult">
<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>ph</th>
      <th>Hardness</th>
      <th>Solids</th>
      <th>Chloramines</th>
      <th>Sulfate</th>
      <th>Conductivity</th>
      <th>Organic_carbon</th>
      <th>Trihalomethanes</th>
      <th>Turbidity</th>
      <th>Potability</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>5.80</td>
      <td>193.20</td>
      <td>19451.77</td>
      <td>4.15</td>
      <td>255.98</td>
      <td>365.48</td>
      <td>14.92</td>
      <td>8.58</td>
      <td>2.18</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>7.78</td>
      <td>196.82</td>
      <td>24789.35</td>
      <td>6.55</td>
      <td>331.04</td>
      <td>372.76</td>
      <td>12.07</td>
      <td>14.34</td>
      <td>5.05</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>6.95</td>
      <td>214.17</td>
      <td>32946.57</td>
      <td>5.48</td>
      <td>333.44</td>
      <td>318.88</td>
      <td>12.81</td>
      <td>15.68</td>
      <td>4.93</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>8.28</td>
      <td>227.65</td>
      <td>17995.41</td>
      <td>7.49</td>
      <td>323.38</td>
      <td>459.87</td>
      <td>14.36</td>
      <td>16.29</td>
      <td>3.69</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>7.06</td>
      <td>191.55</td>
      <td>16473.07</td>
      <td>8.44</td>
      <td>367.85</td>
      <td>462.99</td>
      <td>12.57</td>
      <td>17.53</td>
      <td>3.94</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>
</div>

</div>

</div>

</div>

</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs">
<div class="jp-Cell-inputWrapper">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In&#160;[29]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor">
     <div class="CodeMirror cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="c1">#Importing package</span>
<span class="kn">import</span> <span class="nn">pandas_profiling</span> <span class="k">as</span> <span class="nn">pp</span>
<span class="kn">from</span> <span class="nn">IPython.display</span> <span class="kn">import</span> <span class="n">IFrame</span>
</pre></div>

     </div>
</div>
</div>
</div>

</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In&#160;[7]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor">
     <div class="CodeMirror cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="c1"># Profile Report</span>
<span class="n">dfReport</span> <span class="o">=</span> <span class="n">pp</span><span class="o">.</span><span class="n">ProfileReport</span><span class="p">(</span><span class="n">dataset</span><span class="p">)</span>
<span class="n">dfReport</span><span class="o">.</span><span class="n">to_file</span><span class="p">(</span><span class="s1">&#39;finalReport.html&#39;</span><span class="p">)</span>
<span class="n">display</span><span class="p">(</span><span class="n">IFrame</span><span class="p">(</span><span class="s1">&#39;finalReport.html&#39;</span><span class="p">,</span> <span class="n">width</span><span class="o">=</span><span class="mi">900</span><span class="p">,</span> <span class="n">height</span><span class="o">=</span><span class="mi">350</span><span class="p">))</span>
</pre></div>

     </div>
</div>
</div>
</div>

<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>


<div class="jp-OutputArea jp-Cell-outputArea">

<div class="jp-OutputArea-child">

    
    <div class="jp-OutputPrompt jp-OutputArea-prompt"></div>




<div class="jp-RenderedText jp-OutputArea-output">
<pre>Summarize dataset:   0%|          | 0/5 [00:00&lt;?, ?it/s]</pre>
</div>

</div>

<div class="jp-OutputArea-child">

    
    <div class="jp-OutputPrompt jp-OutputArea-prompt"></div>




<div class="jp-RenderedText jp-OutputArea-output">
<pre>Generate report structure:   0%|          | 0/1 [00:00&lt;?, ?it/s]</pre>
</div>

</div>

<div class="jp-OutputArea-child">

    
    <div class="jp-OutputPrompt jp-OutputArea-prompt"></div>




<div class="jp-RenderedText jp-OutputArea-output">
<pre>Render HTML:   0%|          | 0/1 [00:00&lt;?, ?it/s]</pre>
</div>

</div>

<div class="jp-OutputArea-child">

    
    <div class="jp-OutputPrompt jp-OutputArea-prompt"></div>




<div class="jp-RenderedText jp-OutputArea-output">
<pre>Export report to file:   0%|          | 0/1 [00:00&lt;?, ?it/s]</pre>
</div>

</div>

<div class="jp-OutputArea-child">

    
    <div class="jp-OutputPrompt jp-OutputArea-prompt"></div>



<div class="jp-RenderedHTMLCommon jp-RenderedHTML jp-OutputArea-output">

        <iframe class="d2l-xspl-box" src="https://durhamcollege.desire2learn.com/d2l/lp/externalUrls/xspl?url=finalReport.html" data-original-html="&lt;iframe width=&quot;900&quot; height=&quot;350&quot; src=&quot;finalReport.html&quot; frameborder=&quot;0&quot; allowfullscreen=&quot;&quot;&gt;&lt;/iframe&gt;" frameborder="0" scrolling="no" allowfullscreen></iframe>

        
</div>

</div>

</div>

</div>

</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs">
<div class="jp-Cell-inputWrapper">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In&#160;[30]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor">
     <div class="CodeMirror cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="c1">#Prepare for Models for Comparison</span>

<span class="c1">#Create x and y variables</span>
<span class="n">x</span> <span class="o">=</span> <span class="n">dataset</span><span class="o">.</span><span class="n">drop</span><span class="p">(</span><span class="s1">&#39;Potability&#39;</span><span class="p">,</span> <span class="n">axis</span><span class="o">=</span><span class="mi">1</span><span class="p">)</span><span class="o">.</span><span class="n">to_numpy</span><span class="p">()</span>
<span class="n">Y</span> <span class="o">=</span> <span class="n">dataset</span><span class="p">[</span><span class="s1">&#39;Potability&#39;</span><span class="p">]</span><span class="o">.</span><span class="n">to_numpy</span><span class="p">()</span>

<span class="c1">#Load Library for Training</span>
<span class="kn">from</span> <span class="nn">sklearn.model_selection</span> <span class="kn">import</span> <span class="n">train_test_split</span>
<span class="n">x_train</span><span class="p">,</span><span class="n">x_test</span><span class="p">,</span><span class="n">y_train</span><span class="p">,</span><span class="n">y_test</span> <span class="o">=</span> <span class="n">train_test_split</span><span class="p">(</span><span class="n">x</span><span class="p">,</span><span class="n">Y</span><span class="p">,</span><span class="n">test_size</span> <span class="o">=</span> <span class="mf">0.2</span><span class="p">,</span><span class="n">stratify</span><span class="o">=</span><span class="n">Y</span><span class="p">,</span><span class="n">random_state</span> <span class="o">=</span> <span class="mi">100</span><span class="p">)</span>
</pre></div>

     </div>
</div>
</div>
</div>

</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In&#160;[31]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor">
     <div class="CodeMirror cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="c1"># Use built-in isolation forest</span>
<span class="kn">import</span> <span class="nn">numpy</span> <span class="k">as</span> <span class="nn">np</span>
<span class="kn">from</span> <span class="nn">sklearn.ensemble</span> <span class="kn">import</span> <span class="n">IsolationForest</span>

<span class="c1"># The prediction returns 1 if sample point is inlier. If outlier prediction returns -1</span>
<span class="n">clf_all_features</span> <span class="o">=</span> <span class="n">IsolationForest</span><span class="p">(</span><span class="n">random_state</span><span class="o">=</span><span class="mi">100</span><span class="p">)</span>
<span class="n">clf_all_features</span><span class="o">.</span><span class="n">fit</span><span class="p">(</span><span class="n">x_train</span><span class="p">)</span>

<span class="c1">#Predict if a particular sample is an outlier using all features for higher dimensional data set.</span>
<span class="n">y_pred_train</span> <span class="o">=</span> <span class="n">clf_all_features</span><span class="o">.</span><span class="n">predict</span><span class="p">(</span><span class="n">x_train</span><span class="p">)</span>
<span class="n">y_pred_train2</span> <span class="o">=</span><span class="n">np</span><span class="o">.</span><span class="n">array</span><span class="p">(</span><span class="nb">list</span><span class="p">(</span><span class="nb">map</span><span class="p">(</span><span class="k">lambda</span> <span class="n">x</span><span class="p">:</span> <span class="n">x</span> <span class="o">==</span> <span class="mi">1</span><span class="p">,</span> <span class="n">y_pred_train</span><span class="p">)))</span>

<span class="c1"># Exclude suggested outlier samples for improvement of prediction power/score</span>
<span class="n">x_train_mod</span> <span class="o">=</span> <span class="n">x_train</span><span class="p">[</span><span class="n">y_pred_train2</span><span class="p">,</span> <span class="p">]</span>
<span class="n">y_train_mod</span> <span class="o">=</span> <span class="n">y_train</span><span class="p">[</span><span class="n">y_pred_train2</span><span class="p">,</span> <span class="p">]</span>

<span class="c1">#Size of Datasets</span>
<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;Original Train Dataset Size : </span><span class="si">{}</span><span class="s1">&#39;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="nb">len</span><span class="p">(</span><span class="n">x_train</span><span class="p">)))</span>
<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;New Train Dataset Size      : </span><span class="si">{}</span><span class="s1">&#39;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="nb">len</span><span class="p">(</span><span class="n">x_train_mod</span><span class="p">)))</span>
</pre></div>

     </div>
</div>
</div>
</div>

<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>


<div class="jp-OutputArea jp-Cell-outputArea">

<div class="jp-OutputArea-child">

    
    <div class="jp-OutputPrompt jp-OutputArea-prompt"></div>


<div class="jp-RenderedText jp-OutputArea-output">
<pre>Original Train Dataset Size : 1605
New Train Dataset Size      : 1468
</pre>
</div>
</div>

</div>

</div>

</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs">
<div class="jp-Cell-inputWrapper">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In&#160;[32]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor">
     <div class="CodeMirror cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="c1">#Scale the Data</span>
<span class="kn">from</span> <span class="nn">sklearn.preprocessing</span> <span class="kn">import</span> <span class="n">StandardScaler</span>
<span class="n">sc</span> <span class="o">=</span> <span class="n">StandardScaler</span><span class="p">()</span>
<span class="n">x_train2</span> <span class="o">=</span> <span class="n">sc</span><span class="o">.</span><span class="n">fit_transform</span><span class="p">(</span><span class="n">x_train_mod</span><span class="p">)</span>
<span class="n">x_test2</span> <span class="o">=</span> <span class="n">sc</span><span class="o">.</span><span class="n">fit_transform</span><span class="p">(</span><span class="n">x_test</span><span class="p">)</span>

<span class="n">x_2</span> <span class="o">=</span> <span class="n">sc</span><span class="o">.</span><span class="n">fit_transform</span><span class="p">(</span><span class="n">x</span><span class="p">)</span>

<span class="c1">#Models</span>
<span class="kn">from</span> <span class="nn">sklearn.linear_model</span> <span class="kn">import</span> <span class="n">LogisticRegression</span>
<span class="kn">from</span> <span class="nn">sklearn.naive_bayes</span> <span class="kn">import</span> <span class="n">GaussianNB</span>
</pre></div>

     </div>
</div>
</div>
</div>

</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs">
<div class="jp-Cell-inputWrapper">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In&#160;[33]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor">
     <div class="CodeMirror cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="c1">#Construct some pipelines </span>
<span class="kn">from</span> <span class="nn">sklearn.pipeline</span> <span class="kn">import</span> <span class="n">Pipeline</span>
<span class="kn">from</span> <span class="nn">sklearn.preprocessing</span> <span class="kn">import</span> <span class="n">StandardScaler</span>

<span class="c1">#Create Pipeline</span>

<span class="n">pipeline</span> <span class="o">=</span><span class="p">[]</span>
<span class="n">pipe_gnb</span> <span class="o">=</span> <span class="n">Pipeline</span><span class="p">([(</span><span class="s1">&#39;scl&#39;</span><span class="p">,</span> <span class="n">StandardScaler</span><span class="p">()),</span>
                    <span class="p">(</span><span class="s1">&#39;clf&#39;</span><span class="p">,</span> <span class="n">GaussianNB</span><span class="p">())])</span>

<span class="n">pipeline</span><span class="o">.</span><span class="n">insert</span><span class="p">(</span><span class="mi">0</span><span class="p">,</span><span class="n">pipe_gnb</span><span class="p">)</span>

<span class="n">pipe_logreg</span> <span class="o">=</span> <span class="n">Pipeline</span><span class="p">([(</span><span class="s1">&#39;scl&#39;</span><span class="p">,</span> <span class="n">StandardScaler</span><span class="p">()),</span>
                    <span class="p">(</span><span class="s1">&#39;clf&#39;</span><span class="p">,</span> <span class="n">LogisticRegression</span><span class="p">(</span><span class="n">solver</span><span class="o">=</span><span class="s1">&#39;lbfgs&#39;</span><span class="p">,</span>
                                               <span class="n">class_weight</span><span class="o">=</span><span class="s1">&#39;balanced&#39;</span><span class="p">,</span><span class="n">max_iter</span><span class="o">=</span><span class="mi">1000</span><span class="p">,</span>
                                               <span class="n">random_state</span><span class="o">=</span><span class="mi">100</span><span class="p">))])</span> 
<span class="n">pipeline</span><span class="o">.</span><span class="n">insert</span><span class="p">(</span><span class="mi">1</span><span class="p">,</span><span class="n">pipe_logreg</span><span class="p">)</span>



<span class="c1"># Set grid search params </span>
<span class="n">modelpara</span> <span class="o">=</span> <span class="p">[]</span>

<span class="c1"># Parameter grid for Gaussian Naive Bayes</span>
<span class="n">param_gridgnb</span> <span class="o">=</span> <span class="p">{}</span> <span class="c1"># as there is no hyperparameter for Gaussian Naive</span>
<span class="n">modelpara</span><span class="o">.</span><span class="n">insert</span><span class="p">(</span><span class="mi">0</span><span class="p">,</span> <span class="n">param_gridgnb</span><span class="p">)</span>

<span class="c1"># Parameter grid for Logistic Regression</span>
<span class="n">param_gridlogreg</span> <span class="o">=</span> <span class="p">{</span><span class="s1">&#39;clf__C&#39;</span><span class="p">:</span> <span class="p">[</span><span class="mf">0.01</span><span class="p">,</span> <span class="mf">0.1</span><span class="p">,</span> <span class="mi">1</span><span class="p">,</span> <span class="mi">10</span><span class="p">,</span> <span class="mi">100</span><span class="p">],</span> 
                    <span class="s1">&#39;clf__penalty&#39;</span><span class="p">:</span> <span class="p">[</span><span class="s1">&#39;l2&#39;</span><span class="p">]}</span>
<span class="n">modelpara</span><span class="o">.</span><span class="n">insert</span><span class="p">(</span><span class="mi">1</span><span class="p">,</span> <span class="n">param_gridlogreg</span><span class="p">)</span>
</pre></div>

     </div>
</div>
</div>
</div>

</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs">
<div class="jp-Cell-inputWrapper">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In&#160;[34]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor">
     <div class="CodeMirror cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="c1">#Define Plot for learning curve</span>

<span class="kn">from</span> <span class="nn">sklearn.model_selection</span> <span class="kn">import</span> <span class="n">learning_curve</span>

<span class="k">def</span> <span class="nf">plot_learning_curves</span><span class="p">(</span><span class="n">model</span><span class="p">):</span>
    <span class="n">train_sizes</span><span class="p">,</span> <span class="n">train_scores</span><span class="p">,</span> <span class="n">test_scores</span> <span class="o">=</span> <span class="n">learning_curve</span><span class="p">(</span><span class="n">estimator</span><span class="o">=</span><span class="n">model</span><span class="p">,</span>
                                                            <span class="n">X</span><span class="o">=</span><span class="n">x_train_mod</span><span class="p">,</span> 
                                                            <span class="n">y</span><span class="o">=</span><span class="n">y_train_mod</span><span class="p">,</span>
                                                            <span class="n">train_sizes</span><span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">linspace</span><span class="p">(</span><span class="mf">0.1</span><span class="p">,</span> <span class="mf">1.0</span><span class="p">,</span> <span class="mi">10</span><span class="p">),</span>
                                                            <span class="n">cv</span><span class="o">=</span><span class="mi">10</span><span class="p">,</span><span class="n">scoring</span><span class="o">=</span><span class="s1">&#39;recall_weighted&#39;</span><span class="p">,</span><span class="n">random_state</span><span class="o">=</span><span class="mi">100</span><span class="p">)</span>
    <span class="n">train_mean</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">mean</span><span class="p">(</span><span class="n">train_scores</span><span class="p">,</span> <span class="n">axis</span><span class="o">=</span><span class="mi">1</span><span class="p">)</span>
    <span class="n">train_std</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">std</span><span class="p">(</span><span class="n">train_scores</span><span class="p">,</span> <span class="n">axis</span><span class="o">=</span><span class="mi">1</span><span class="p">)</span>
    <span class="n">test_mean</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">mean</span><span class="p">(</span><span class="n">test_scores</span><span class="p">,</span> <span class="n">axis</span><span class="o">=</span><span class="mi">1</span><span class="p">)</span>
    <span class="n">test_std</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">std</span><span class="p">(</span><span class="n">test_scores</span><span class="p">,</span> <span class="n">axis</span><span class="o">=</span><span class="mi">1</span><span class="p">)</span>
    
    <span class="n">plt</span><span class="o">.</span><span class="n">plot</span><span class="p">(</span><span class="n">train_sizes</span><span class="p">,</span> <span class="n">train_mean</span><span class="p">,</span><span class="n">color</span><span class="o">=</span><span class="s1">&#39;blue&#39;</span><span class="p">,</span> <span class="n">marker</span><span class="o">=</span><span class="s1">&#39;o&#39;</span><span class="p">,</span> 
             <span class="n">markersize</span><span class="o">=</span><span class="mi">5</span><span class="p">,</span> <span class="n">label</span><span class="o">=</span><span class="s1">&#39;training accuracy&#39;</span><span class="p">)</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">fill_between</span><span class="p">(</span><span class="n">train_sizes</span><span class="p">,</span> <span class="n">train_mean</span> <span class="o">+</span> <span class="n">train_std</span><span class="p">,</span> <span class="n">train_mean</span> <span class="o">-</span> <span class="n">train_std</span><span class="p">,</span>
                     <span class="n">alpha</span><span class="o">=</span><span class="mf">0.15</span><span class="p">,</span> <span class="n">color</span><span class="o">=</span><span class="s1">&#39;blue&#39;</span><span class="p">)</span>

    <span class="n">plt</span><span class="o">.</span><span class="n">plot</span><span class="p">(</span><span class="n">train_sizes</span><span class="p">,</span> <span class="n">test_mean</span><span class="p">,</span> <span class="n">color</span><span class="o">=</span><span class="s1">&#39;green&#39;</span><span class="p">,</span> <span class="n">linestyle</span><span class="o">=</span><span class="s1">&#39;--&#39;</span><span class="p">,</span> <span class="n">marker</span><span class="o">=</span><span class="s1">&#39;s&#39;</span><span class="p">,</span> <span class="n">markersize</span><span class="o">=</span><span class="mi">5</span><span class="p">,</span>
             <span class="n">label</span><span class="o">=</span><span class="s1">&#39;validation accuracy&#39;</span><span class="p">)</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">fill_between</span><span class="p">(</span><span class="n">train_sizes</span><span class="p">,</span> <span class="n">test_mean</span> <span class="o">+</span> <span class="n">test_std</span><span class="p">,</span> <span class="n">test_mean</span> <span class="o">-</span> <span class="n">test_std</span><span class="p">,</span>
                     <span class="n">alpha</span><span class="o">=</span><span class="mf">0.15</span><span class="p">,</span> <span class="n">color</span><span class="o">=</span><span class="s1">&#39;green&#39;</span><span class="p">)</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">grid</span><span class="p">(</span><span class="kc">True</span><span class="p">)</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">xlabel</span><span class="p">(</span><span class="s1">&#39;Number of training samples&#39;</span><span class="p">)</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">ylabel</span><span class="p">(</span><span class="s1">&#39;Recall&#39;</span><span class="p">)</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">legend</span><span class="p">(</span><span class="n">loc</span><span class="o">=</span><span class="s1">&#39;best&#39;</span><span class="p">)</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">ylim</span><span class="p">([</span><span class="mf">0.0</span><span class="p">,</span> <span class="mf">1.01</span><span class="p">])</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">show</span><span class="p">()</span>
</pre></div>

     </div>
</div>
</div>
</div>

</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In&#160;[35]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor">
     <div class="CodeMirror cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="c1">#Plot Learning Curve</span>
<span class="o">%</span><span class="k">matplotlib</span> inline
<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;NaiveBayes Learning Curve&#39;</span><span class="p">)</span>
<span class="n">plot_learning_curves</span><span class="p">(</span><span class="n">pipe_gnb</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;</span><span class="se">\n</span><span class="s1"> LogisticRegression Learning Curve&#39;</span><span class="p">)</span>
<span class="n">plot_learning_curves</span><span class="p">(</span><span class="n">pipe_logreg</span><span class="p">)</span>
</pre></div>

     </div>
</div>
</div>
</div>

<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>


<div class="jp-OutputArea jp-Cell-outputArea">

<div class="jp-OutputArea-child">

    
    <div class="jp-OutputPrompt jp-OutputArea-prompt"></div>


<div class="jp-RenderedText jp-OutputArea-output">
<pre>NaiveBayes Learning Curve
</pre>
</div>
</div>

<div class="jp-OutputArea-child">

    
    <div class="jp-OutputPrompt jp-OutputArea-prompt"></div>




<div class="jp-RenderedImage jp-OutputArea-output">
<img src="javascript://"/>
</div>

</div>

<div class="jp-OutputArea-child">

    
    <div class="jp-OutputPrompt jp-OutputArea-prompt"></div>


<div class="jp-RenderedText jp-OutputArea-output">
<pre>
 LogisticRegression Learning Curve
</pre>
</div>
</div>

<div class="jp-OutputArea-child">

    
    <div class="jp-OutputPrompt jp-OutputArea-prompt"></div>




<div class="jp-RenderedImage jp-OutputArea-output">
<img src="javascript://"/>
</div>

</div>

</div>

</div>

</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs">
<div class="jp-Cell-inputWrapper">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In&#160;[36]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor">
     <div class="CodeMirror cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="c1">#Define Gridsearch Function</span>

<span class="kn">from</span> <span class="nn">sklearn.model_selection</span> <span class="kn">import</span> <span class="n">GridSearchCV</span>
<span class="kn">from</span> <span class="nn">sklearn.metrics</span> <span class="kn">import</span> <span class="n">classification_report</span><span class="p">,</span> <span class="n">confusion_matrix</span>
<span class="kn">from</span> <span class="nn">sklearn.metrics</span> <span class="kn">import</span> <span class="n">roc_curve</span><span class="p">,</span> <span class="n">auc</span>
<span class="kn">from</span> <span class="nn">sklearn.metrics</span> <span class="kn">import</span> <span class="n">roc_auc_score</span>

<span class="k">def</span> <span class="nf">Gridsearch_cv</span><span class="p">(</span><span class="n">model</span><span class="p">,</span> <span class="n">params</span><span class="p">):</span>
    
    <span class="c1">#Cross-validation Function</span>
    <span class="n">cv2</span><span class="o">=</span><span class="n">RepeatedKFold</span><span class="p">(</span><span class="n">n_splits</span><span class="o">=</span><span class="mi">10</span><span class="p">,</span> <span class="n">n_repeats</span><span class="o">=</span><span class="mi">5</span><span class="p">,</span> <span class="n">random_state</span><span class="o">=</span><span class="mi">100</span><span class="p">)</span>
        
    <span class="c1">#GridSearch CV</span>
    <span class="n">gs_clf</span> <span class="o">=</span> <span class="n">GridSearchCV</span><span class="p">(</span><span class="n">model</span><span class="p">,</span> <span class="n">params</span><span class="p">,</span> <span class="n">cv</span><span class="o">=</span><span class="n">cv2</span><span class="p">,</span><span class="n">scoring</span><span class="o">=</span><span class="s1">&#39;recall_weighted&#39;</span><span class="p">)</span>
    <span class="n">gs_clf</span> <span class="o">=</span> <span class="n">gs_clf</span><span class="o">.</span><span class="n">fit</span><span class="p">(</span><span class="n">x_train_mod</span><span class="p">,</span> <span class="n">y_train_mod</span><span class="p">)</span>
    <span class="n">model</span> <span class="o">=</span> <span class="n">gs_clf</span><span class="o">.</span><span class="n">best_estimator_</span>
    
    <span class="c1"># Use best model and test data for final evaluation</span>
    <span class="n">y_pred</span> <span class="o">=</span> <span class="n">model</span><span class="o">.</span><span class="n">predict</span><span class="p">(</span><span class="n">x_test2</span><span class="p">)</span>
    <span class="c1">#Identify Best Parameters to Optimize the Model</span>
    <span class="n">bestpara</span><span class="o">=</span><span class="nb">str</span><span class="p">(</span><span class="n">gs_clf</span><span class="o">.</span><span class="n">best_params_</span><span class="p">)</span>
    
    <span class="c1">#Output Heading</span>
    <span class="nb">print</span><span class="p">(</span><span class="s1">&#39;</span><span class="se">\n</span><span class="s1">Optimized Model&#39;</span><span class="p">)</span>
    <span class="nb">print</span><span class="p">(</span><span class="s1">&#39;</span><span class="se">\n</span><span class="s1">Model Name:&#39;</span><span class="p">,</span><span class="nb">str</span><span class="p">(</span><span class="n">pipeline</span><span class="o">.</span><span class="n">named_steps</span><span class="p">[</span><span class="s1">&#39;clf&#39;</span><span class="p">]))</span>
        
    
<span class="c1">#Output Validation Statistics</span>
    <span class="nb">print</span><span class="p">(</span><span class="s1">&#39;</span><span class="se">\n</span><span class="s1">Best Parameters:&#39;</span><span class="p">,</span><span class="n">bestpara</span><span class="p">)</span>
    <span class="nb">print</span><span class="p">(</span><span class="s1">&#39;</span><span class="se">\n</span><span class="s1">&#39;</span><span class="p">,</span> <span class="n">confusion_matrix</span><span class="p">(</span><span class="n">y_test</span><span class="p">,</span><span class="n">y_pred</span><span class="p">))</span>  
    <span class="nb">print</span><span class="p">(</span><span class="s1">&#39;</span><span class="se">\n</span><span class="s1">&#39;</span><span class="p">,</span><span class="n">classification_report</span><span class="p">(</span><span class="n">y_test</span><span class="p">,</span><span class="n">y_pred</span><span class="p">))</span>     
    
    <span class="c1">#Setup the ROC Curve</span>
    <span class="kn">from</span> <span class="nn">sklearn.metrics</span> <span class="kn">import</span> <span class="n">roc_curve</span><span class="p">,</span> <span class="n">auc</span>
    <span class="kn">from</span> <span class="nn">sklearn</span> <span class="kn">import</span> <span class="n">metrics</span>
    <span class="n">fpr</span><span class="p">,</span> <span class="n">tpr</span><span class="p">,</span> <span class="n">threshold</span> <span class="o">=</span> <span class="n">metrics</span><span class="o">.</span><span class="n">roc_curve</span><span class="p">(</span><span class="n">y_test</span><span class="p">,</span> <span class="n">y_pred</span><span class="p">)</span>
    <span class="n">roc_auc</span> <span class="o">=</span> <span class="n">metrics</span><span class="o">.</span><span class="n">auc</span><span class="p">(</span><span class="n">fpr</span><span class="p">,</span> <span class="n">tpr</span><span class="p">)</span>
    <span class="nb">print</span><span class="p">(</span><span class="s1">&#39;ROC Curve&#39;</span><span class="p">)</span>
    
    <span class="c1">#Plot the ROC Curve</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">title</span><span class="p">(</span><span class="s1">&#39;Receiver Operating Characteristic&#39;</span><span class="p">)</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">plot</span><span class="p">(</span><span class="n">fpr</span><span class="p">,</span> <span class="n">tpr</span><span class="p">,</span> <span class="s1">&#39;b&#39;</span><span class="p">,</span> <span class="n">label</span> <span class="o">=</span> <span class="s1">&#39;AUC = </span><span class="si">%0.2f</span><span class="s1">&#39;</span> <span class="o">%</span> <span class="n">roc_auc</span><span class="p">)</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">legend</span><span class="p">(</span><span class="n">loc</span> <span class="o">=</span> <span class="s1">&#39;lower right&#39;</span><span class="p">)</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">plot</span><span class="p">([</span><span class="mi">0</span><span class="p">,</span> <span class="mi">1</span><span class="p">],</span> <span class="p">[</span><span class="mi">0</span><span class="p">,</span> <span class="mi">1</span><span class="p">],</span><span class="s1">&#39;r--&#39;</span><span class="p">)</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">xlim</span><span class="p">([</span><span class="mi">0</span><span class="p">,</span> <span class="mi">1</span><span class="p">])</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">ylim</span><span class="p">([</span><span class="mi">0</span><span class="p">,</span> <span class="mi">1</span><span class="p">])</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">ylabel</span><span class="p">(</span><span class="s1">&#39;True Positive Rate&#39;</span><span class="p">)</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">xlabel</span><span class="p">(</span><span class="s1">&#39;False Positive Rate&#39;</span><span class="p">)</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">show</span><span class="p">()</span>
</pre></div>

     </div>
</div>
</div>
</div>

</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In&#160;[37]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor">
     <div class="CodeMirror cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="c1">#Run Models</span>
<span class="kn">from</span> <span class="nn">sklearn.model_selection</span> <span class="kn">import</span> <span class="n">RepeatedKFold</span>

<span class="k">for</span> <span class="n">pipeline</span><span class="p">,</span> <span class="n">modelpara</span> <span class="ow">in</span> <span class="nb">zip</span><span class="p">(</span><span class="n">pipeline</span><span class="p">,</span> <span class="n">modelpara</span><span class="p">):</span>
    <span class="n">Gridsearch_cv</span><span class="p">(</span><span class="n">pipeline</span><span class="p">,</span> <span class="n">modelpara</span><span class="p">)</span>
</pre></div>

     </div>
</div>
</div>
</div>

<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>


<div class="jp-OutputArea jp-Cell-outputArea">

<div class="jp-OutputArea-child">

    
    <div class="jp-OutputPrompt jp-OutputArea-prompt"></div>


<div class="jp-RenderedText jp-OutputArea-output">
<pre>
Optimized Model

Model Name: GaussianNB()

Best Parameters: {}

 [[  0 240]
 [  0 162]]
</pre>
</div>
</div>

<div class="jp-OutputArea-child">

    
    <div class="jp-OutputPrompt jp-OutputArea-prompt"></div>


<div class="jp-RenderedText jp-OutputArea-output">
<pre>E:\AnshCollege\lib\site-packages\sklearn\metrics\_classification.py:1318: UndefinedMetricWarning: Precision and F-score are ill-defined and being set to 0.0 in labels with no predicted samples. Use `zero_division` parameter to control this behavior.
  _warn_prf(average, modifier, msg_start, len(result))
E:\AnshCollege\lib\site-packages\sklearn\metrics\_classification.py:1318: UndefinedMetricWarning: Precision and F-score are ill-defined and being set to 0.0 in labels with no predicted samples. Use `zero_division` parameter to control this behavior.
  _warn_prf(average, modifier, msg_start, len(result))
E:\AnshCollege\lib\site-packages\sklearn\metrics\_classification.py:1318: UndefinedMetricWarning: Precision and F-score are ill-defined and being set to 0.0 in labels with no predicted samples. Use `zero_division` parameter to control this behavior.
  _warn_prf(average, modifier, msg_start, len(result))
</pre>
</div>
</div>

<div class="jp-OutputArea-child">

    
    <div class="jp-OutputPrompt jp-OutputArea-prompt"></div>


<div class="jp-RenderedText jp-OutputArea-output">
<pre>
               precision    recall  f1-score   support

           0       0.00      0.00      0.00       240
           1       0.40      1.00      0.57       162

    accuracy                           0.40       402
   macro avg       0.20      0.50      0.29       402
weighted avg       0.16      0.40      0.23       402

ROC Curve
</pre>
</div>
</div>

<div class="jp-OutputArea-child">

    
    <div class="jp-OutputPrompt jp-OutputArea-prompt"></div>




<div class="jp-RenderedImage jp-OutputArea-output">
<img src="javascript://"/>
</div>

</div>

<div class="jp-OutputArea-child">

    
    <div class="jp-OutputPrompt jp-OutputArea-prompt"></div>


<div class="jp-RenderedText jp-OutputArea-output">
<pre>
Optimized Model

Model Name: LogisticRegression(class_weight=&#39;balanced&#39;, max_iter=1000, random_state=100)

Best Parameters: {&#39;clf__C&#39;: 0.01, &#39;clf__penalty&#39;: &#39;l2&#39;}

 [[240   0]
 [162   0]]

               precision    recall  f1-score   support

           0       0.60      1.00      0.75       240
           1       0.00      0.00      0.00       162

    accuracy                           0.60       402
   macro avg       0.30      0.50      0.37       402
weighted avg       0.36      0.60      0.45       402

ROC Curve
</pre>
</div>
</div>

<div class="jp-OutputArea-child">

    
    <div class="jp-OutputPrompt jp-OutputArea-prompt"></div>


<div class="jp-RenderedText jp-OutputArea-output">
<pre>E:\AnshCollege\lib\site-packages\sklearn\metrics\_classification.py:1318: UndefinedMetricWarning: Precision and F-score are ill-defined and being set to 0.0 in labels with no predicted samples. Use `zero_division` parameter to control this behavior.
  _warn_prf(average, modifier, msg_start, len(result))
E:\AnshCollege\lib\site-packages\sklearn\metrics\_classification.py:1318: UndefinedMetricWarning: Precision and F-score are ill-defined and being set to 0.0 in labels with no predicted samples. Use `zero_division` parameter to control this behavior.
  _warn_prf(average, modifier, msg_start, len(result))
E:\AnshCollege\lib\site-packages\sklearn\metrics\_classification.py:1318: UndefinedMetricWarning: Precision and F-score are ill-defined and being set to 0.0 in labels with no predicted samples. Use `zero_division` parameter to control this behavior.
  _warn_prf(average, modifier, msg_start, len(result))
</pre>
</div>
</div>

<div class="jp-OutputArea-child">

    
    <div class="jp-OutputPrompt jp-OutputArea-prompt"></div>




<div class="jp-RenderedImage jp-OutputArea-output">
<img src="javascript://"/>
</div>

</div>

</div>

</div>

</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In&#160;[40]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor">
     <div class="CodeMirror cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="kn">from</span> <span class="nn">sklearn.ensemble</span> <span class="kn">import</span> <span class="n">VotingClassifier</span>
<span class="kn">from</span> <span class="nn">sklearn.model_selection</span> <span class="kn">import</span> <span class="n">RepeatedKFold</span>
<span class="kn">from</span> <span class="nn">sklearn.model_selection</span> <span class="kn">import</span> <span class="n">cross_validate</span>
<span class="kn">from</span> <span class="nn">sklearn.ensemble</span> <span class="kn">import</span> <span class="n">BaggingClassifier</span>

<span class="n">estimators</span> <span class="o">=</span> <span class="p">[]</span>
<span class="n">model1</span> <span class="o">=</span> <span class="n">GaussianNB</span><span class="p">()</span>
<span class="n">estimators</span><span class="o">.</span><span class="n">append</span><span class="p">((</span><span class="s1">&#39;Naive Bayes&#39;</span><span class="p">,</span> <span class="n">model1</span><span class="p">))</span>
<span class="n">model2</span> <span class="o">=</span> <span class="n">GradientBoostingClassifier</span><span class="p">(</span><span class="n">random_state</span><span class="o">=</span><span class="mi">100</span><span class="p">)</span>
<span class="n">estimators</span><span class="o">.</span><span class="n">append</span><span class="p">((</span><span class="s1">&#39;Gradient Boosting&#39;</span><span class="p">,</span> <span class="n">model2</span><span class="p">))</span>
<span class="n">voting_clf</span><span class="o">=</span><span class="n">VotingClassifier</span><span class="p">(</span><span class="n">estimators</span><span class="p">,</span><span class="n">voting</span><span class="o">=</span><span class="s1">&#39;soft&#39;</span><span class="p">)</span>

<span class="n">scoring</span> <span class="o">=</span> <span class="p">{</span><span class="s1">&#39;acc&#39;</span><span class="p">:</span> <span class="s1">&#39;accuracy&#39;</span><span class="p">,</span>
           <span class="s1">&#39;prec_macro&#39;</span><span class="p">:</span> <span class="s1">&#39;precision_macro&#39;</span><span class="p">,</span>
           <span class="s1">&#39;rec_macro&#39;</span><span class="p">:</span> <span class="s1">&#39;recall_macro&#39;</span><span class="p">}</span>
<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;</span><span class="se">\n</span><span class="s1">Voting Model&#39;</span><span class="p">)</span>
<span class="k">for</span> <span class="n">clf</span> <span class="ow">in</span> <span class="p">(</span><span class="n">model1</span><span class="p">,</span><span class="n">model2</span><span class="p">,</span><span class="n">voting_clf</span><span class="p">):</span>
    <span class="n">rkfcv</span><span class="o">=</span> <span class="n">clf</span><span class="o">.</span><span class="n">fit</span><span class="p">(</span><span class="n">x_train2</span><span class="p">,</span><span class="n">y_train_mod</span><span class="p">)</span>
    <span class="n">ens_rkf1</span> <span class="o">=</span> <span class="n">RepeatedKFold</span><span class="p">(</span><span class="n">n_splits</span><span class="o">=</span><span class="mi">10</span><span class="p">,</span> <span class="n">n_repeats</span><span class="o">=</span><span class="mi">5</span><span class="p">,</span> <span class="n">random_state</span><span class="o">=</span><span class="mi">100</span><span class="p">)</span>
    <span class="n">rKFcv</span> <span class="o">=</span> <span class="n">cross_validate</span><span class="p">(</span><span class="n">rkfcv</span><span class="p">,</span> <span class="n">x_2</span><span class="p">,</span> <span class="n">Y</span><span class="p">,</span> <span class="n">scoring</span><span class="o">=</span><span class="n">scoring</span><span class="p">,</span> <span class="n">cv</span><span class="o">=</span><span class="n">ens_rkf1</span><span class="p">)</span>
    <span class="nb">print</span><span class="p">(</span><span class="n">clf</span><span class="o">.</span><span class="vm">__class__</span><span class="o">.</span><span class="vm">__name__</span><span class="p">,</span><span class="nb">round</span><span class="p">(</span><span class="n">rKFcv</span><span class="p">[</span><span class="s1">&#39;test_rec_macro&#39;</span><span class="p">]</span><span class="o">.</span><span class="n">mean</span><span class="p">(),</span><span class="mi">2</span><span class="p">))</span>
</pre></div>

     </div>
</div>
</div>
</div>

<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>


<div class="jp-OutputArea jp-Cell-outputArea">

<div class="jp-OutputArea-child">

    
    <div class="jp-OutputPrompt jp-OutputArea-prompt"></div>


<div class="jp-RenderedText jp-OutputArea-output">
<pre>
Voting Model
GaussianNB 0.56
GradientBoostingClassifier 0.59
VotingClassifier 0.59
</pre>
</div>
</div>

</div>

</div>

</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs">
<div class="jp-Cell-inputWrapper">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In&#160;[&#160;]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor">
     <div class="CodeMirror cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span> 
</pre></div>

     </div>
</div>
</div>
</div>

</div>









<script type="module" src="https://s.brightspace.com/lib/bsi/2024.10.209/unbundled/mathjax.js"></script><script type="text/javascript">document.addEventListener('DOMContentLoaded', function() {
						if (document.querySelector('math') || /\$\$|\\\(|\\\[|\\begin{|\\ref{|\\eqref{/.test(document.body.innerHTML)) {
							document.querySelectorAll('mspace[linebreak="newline"]').forEach(elm => {
								elm.setAttribute('style', 'display: block; height: 0.5rem;');
							});

							window.D2L.MathJax.loadMathJax({
								outputScale: 1.5,
								renderLatex: false,
								enableMML3Support: false
							});
						}
					});</script><script type="module" src="https://s.brightspace.com/lib/bsi/2024.10.209/unbundled/prism.js"></script><script type="text/javascript">document.addEventListener('DOMContentLoaded', function() {
					document.querySelectorAll('.d2l-code').forEach(code => {
						window.D2L.Prism.formatCodeElement(code);
					});
				});</script><script type="module" src="https://s.brightspace.com/lib/bsi/2024.10.209/unbundled/embeds.js"></script><script type="text/javascript">document.addEventListener('DOMContentLoaded', function() {
					window.D2L.EmbedRenderer.renderEmbeds(document.body);
				});</script></body></html>tml…]()
