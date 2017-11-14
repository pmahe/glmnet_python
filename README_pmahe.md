
A fork to fix a few bugs / versioning issues : 

* problem in **cvglmnet()** function : 
  * line 260 : ma = scipy.tile(scipy.arange(nfolds), [1, scipy.floor(nobs/nfolds)]) 
  * problem : scipy.floor(nobs/nfolds) returned a float variable, that scipy.tile() does not like
  * fix : ma = scipy.tile(scipy.arange(nfolds), [1, int(scipy.floor(nobs/nfolds))])

* problem passing the "mtype=grouped" option to **glmnet()** function (for multinomial models) 
  * **TODO** : check how the option is dealt with for **cvglmnet()**
 
 * re-formating of the matrix of predictions for multinomial models
   * a big matrix of size $n \times K \times n_{\lambda}$ 
   * change into $n_{\lambda}$ matrices of size $n \times K$
   * **NB : should be done as R version --> to check**

 * issue in passing "auc" option to **cvglmnet()**
 
