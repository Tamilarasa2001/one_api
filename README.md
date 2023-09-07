# one_api
Intel-Workshop-Task_one api
Intel-Workshop-Tasks This is machine learning task files for Intel OneAPI Workshop.

I was getting same error over and over. The scikit learn library is not working in my dev cloud environment. Couldn't complete the tasks.

The Error message as follows:

RuntimeError Traceback (most recent call last) RuntimeError: module compiled against API version 0x10 but this version of numpy is 0xf

The above exception was the direct cause of the following exception:

SystemError Traceback (most recent call last) Cell In[5], line 1 ----> 1 from sklearn import preprocessing 2 # Step 2 - Convert Gender to number 3 from sklearn.preprocessing import LabelEncoder

File /opt/intel/inteloneapi/intelpython/latest/lib/python3.9/site-packages/sklearn/init.py:80 69 sys.stderr.write("Partial import of sklearn during the build process.\n") 70 # We are not importing the rest of scikit-learn during the build 71 # process, as it may not be compiled yet 72 else: (...) 78 # later is linked to the OpenMP runtime to make it possible to introspect 79 # it and importing it first would fail if the OpenMP dll cannot be found. ---> 80 from . import _distributor_init # noqa: F401 81 from . import __check_build # noqa: F401 82 from .base import clone

File /opt/intel/inteloneapi/intelpython/latest/lib/python3.9/site-packages/sklearn/_distributor_init.py:13 1 """ Distributor init file 2 3 Distributors: you can add custom code here to support particular distributions (...) 9 so you can safely replace this file with your own version. 10 """ 12 try: ---> 13 from sklearnex import patch_sklearn 14 patch_sklearn(name=None, verbose=True) 15 del patch_sklearn

File /opt/intel/inteloneapi/intelpython/latest/lib/python3.9/site-packages/sklearnex/init.py:18 1 #!/usr/bin/env python 2 #=============================================================================== 3 # Copyright 2021 Intel Corporation (...) 15 # limitations under the License. 16 #=============================================================================== ---> 18 from .dispatcher import patch_sklearn 19 from .dispatcher import unpatch_sklearn 20 from .dispatcher import get_patch_names

File /opt/intel/inteloneapi/intelpython/latest/lib/python3.9/site-packages/sklearnex/dispatcher.py:22 20 import os 21 from functools import lru_cache ---> 22 from daal4py.sklearn._utils import daal_check_version, sklearn_check_version 25 def _is_new_patching_available(): 26 return os.environ.get('OFF_ONEDAL_IFACE') is None 27 and daal_check_version((2021, 'P', 300))

File /opt/intel/inteloneapi/intelpython/latest/lib/python3.9/site-packages/daal4py/sklearn/init.py:17 1 #=============================================================================== 2 # Copyright 2014 Intel Corporation 3 # (...) 14 # limitations under the License. 15 #=============================================================================== ---> 17 from .monkeypatch.dispatcher import enable as patch_sklearn 18 from .monkeypatch.dispatcher import disable as unpatch_sklearn 19 from .monkeypatch.dispatcher import patch_is_enabled as sklearn_is_patched

File /opt/intel/inteloneapi/intelpython/latest/lib/python3.9/site-packages/daal4py/sklearn/monkeypatch/dispatcher.py:21 19 from ..neighbors import NearestNeighbors as NearestNeighbors_daal4py 20 from ..neighbors import KNeighborsClassifier as KNeighborsClassifier_daal4py ---> 21 from ..model_selection import _daal_train_test_split 22 from ..utils.validation import _daal_assert_all_finite 23 from ..svm.svm import SVC as SVC_daal4py

File /opt/intel/inteloneapi/intelpython/latest/lib/python3.9/site-packages/daal4py/sklearn/model_selection/init.py:17 1 #=============================================================================== 2 # Copyright 2014 Intel Corporation 3 # (...) 14 # limitations under the License. 15 #=============================================================================== ---> 17 from ._split import _daal_train_test_split 19 all = ['_daal_train_test_split']

File /opt/intel/inteloneapi/intelpython/latest/lib/python3.9/site-packages/daal4py/sklearn/model_selection/_split.py:34 31 from sklearn.utils import safe_indexing 33 try: ---> 34 import mkl_random 35 mkl_random_is_imported = True 36 except (ImportError, ModuleNotFoundError):

File /opt/intel/inteloneapi/intelpython/latest/lib/python3.9/site-packages/mkl_random/init.py:29 1 #!/usr/bin/env python 2 # Copyright (c) 2017-2019, Intel Corporation 3 # (...) 24 # OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE 25 # OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE. 27 from future import division, absolute_import, print_function ---> 29 from .mklrand import * 30 from ._version import version 32 try:

File mkl_random/mklrand.pyx:188, in init mkl_random.mklrand()

SystemError: <class 'ImportError'> returned a result with an error set
