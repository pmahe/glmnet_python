
A fork to fix a few bugs / versioning issues : 

* problem in **cvglmnet()** function : cross-validation does not work
  * line 260 : *ma = scipy.tile(scipy.arange(nfolds), [1, scipy.floor(nobs/nfolds)])*
  * problem : *scipy.floor(nobs/nfolds)* returned a float variable, that *scipy.tile()* does not like
  * fix : *ma = scipy.tile(scipy.arange(nfolds), [1, int(scipy.floor(nobs/nfolds))])*

* problem passing the "mtype=grouped" option to **glmnet()** function (for multinomial models) 
  * line 424 : *elif (indm == 2)* changed into *elif (indm\[0\] == 1)*
   * (we need to check if the 1st (and single) element of 'indm' is equal to the 2nd element of the 'mtypelist' defined a couple of lines before)
  * **TODO** : check how the option is dealt with for **cvglmnet()**
 
 * problem in the output of **glmnetPredict()** with model of *family='multinomial', when *ptype='class'*
   * problem : output provided = a vector of length (Nsamples x Nlambda), while should be a matrix of size \[Nsamples x Nlambdas\], for consistency with R interface
   * fix : reshape of result by *result = scipy.reshape(result, (-1,dp.shape[2]), order = 'F')* at line 258
   * (NB : works when *ptype='link'* or *ptype='response'*  : output = an array of size \[Nsamples x Nclasses x Nlambdas \]


 * issue in passing "auc" option to **cvglmnet()**
   * **TODO** : investigate !
 
