# SSP-FILE-for-datatable-

$dataSourceObject = ConnectionManager::get('default');
$table = 'eb_deal_pipeline';
$primaryKey = 'id';
$extraWhere = '';
$joinQuery = '';

$columns = array(
    array('db' => "name", 'dt' => 0, 'field' => 'name'),
    array('db' => 'id', 'dt' => 1, 'field' => 'id',
        'formatter' => function($d, $row) {
            return $this->countAssociatedstage($d);
        }),
    array('db' => 'id', 'dt' => 2, 'field' => 'id',
        'formatter' => function($d, $row) {
            return $this->pipelineAction($d);
        }),
    array('db' => 'id', 'dt' => 3, 'field' => 'id', 
        'formatter' => function($d, $row) {
            return intval($d);
        })
    );

$sql_details = array(
    'user' => $dataSourceObject->config()['username'],
    'pass' => $dataSourceObject->config()['password'],
    'db' => $dataSourceObject->config()['database'],
    'host' => $dataSourceObject->config()['host']
    );

echo json_encode(
    CustomeSSP::simple($_GET, $sql_details, $table, $primaryKey, $columns, $joinQuery, $extraWhere)
    );
die;


