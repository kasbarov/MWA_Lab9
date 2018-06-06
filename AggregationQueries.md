1. db.zips.aggregate([
{$match: {state :'IA'}},
{$project: {_id:1}}
])

2. db.zips.aggregate([
{$match: {pop :{$lt:1000}}},
{$project: {_id:1}}
])

3. db.zips.aggregate ([
{$group: {_id:{'state':'$state', 'city':'$city'}, num_zips: {$sum:1}}},
{$match: {num_zips:{$gt:1}}},
{$sort:{state:1, _id:1}}
])

4.  db.zips.aggregate ([
{$group:{_id:{'state':'$state', 'city':'$city'}, population: {$sum:'$pop'}}},
{$sort: {'_id.state':1, 'population':1}},
{$group: {_id:'$_id.state',city: {'$first':'$_id.city'}, population: {'$first':'$population'}}}
])

