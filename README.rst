Python & Pandas support for SiteCatalyst, part of Adobe's Marketing Cloud.

Python support for the SiteCatalyst API.

Pandas integration for pulling reports directly into Pandas DataFrame's.

Pandas example usage::

    from sitecat_py.pandas_api import SiteCatPandas
    
    username = 'my_username'
    secret = 'my_shared_secret''
    sc_pd = SiteCatPandas(username, secret)

    df = sc_pd.read_sc(report_suite_id='my_report_suite',
                       date_from='2015-04-01',
                       date_to='2015-04-02',
                       metrics=['visits', 'pageviews'],
                       date_granularity='day',
                       elements=['prop2'])

    print df.head()

   
Python example usage::

    from sitecat_py.python_api import SiteCatPy
    from sitecat_py.pandas_api import SiteCatPandas

    sc_py = SiteCatPy(username, secret)

    method = 'ReportSuite.GetSegments'
    request_data = {
        "rsid_list": ["my_reportsuite"],
    }
    json_data = sc_py.make_request(method, request_data)

    ####
    request_data = {
        report_description = {
            "reportSuiteID": "my_reportsuite",
            "dateFrom": "2013-04-01",
            "dateTo": "2013-04-03",
            "dateGranularity": "day",
            "metrics": [{"id": "visits"}],
            "elements": [{"id": "page"}],
            #"elements": [{"id": "product", "classification": "Product Category"}],
        },
        'validate': 1,
    }
    json_data = sc_py.make_queued_request('Report.QueueTrended', request_data)
    df = SiteCatPandas.df_from_sitecat_raw(json_data)
    ####
    json_data = sc_py.get_report(request_data['report_description'])
