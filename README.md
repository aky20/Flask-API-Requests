# Flask-API-Requests
## jsonify()

## GET (get all post)
```
from flask import Flask, jsonify, render_template, request

@app.route("/all")
def get_all_post():
    return jsonify(posts)
```
-------------------------------------
## POST (add new post)
```
@app.route("/add", methods=['POST'])
def add():
    new_post = Post(
        title = request.form["title"],
        content = request.form["content"],
        )
    db.session.add(new_post)
    db.session.commit()
    return jsonify({"success": "Successfully added."})
```
---------------------------------------
## PUT (update all data that match with id)
```
@app.route("/update/<id>", methods=['PUT'])
def update(id):
    # get post that match with requested id
    post = Post.query.get(request.args['id'])
    
    if post:
      # update data
      post.title = request.form['title']
      post.content = request.form['content']
      db.session.add(post)
      db.session.commit()
      return jsonify({"success": "Successfully updated"})
    else:
      return jsonify({"error": "not found id"})
```
--------------------------------------
## PATCH (update only title that match with id)
```
@app.route("/update-title/<id>", methods=['PATCH'])
def update_title(id):
    post = Post.query.get(id)
    if post:
        try:
            # get title parameter in url
            post.title = request.args["title"]
        except:
            return jsonify({"error": "you must pass title as parameter"})
        else:
            db.session.commit()
            return jsonify({"success": "Successfully updated"})
    else:
        return jsonify({"error": "not found id"})
```
-------------------------------------------
## DELETE (delete post)
```
@app.route("/delete/<id>", methods=['DELETE'])
def delete(id):
    post = Post.query.get(id)
    db.session.delete(cafe)
    db.session.commit()
    return jsonify({"success": "successfully deleted"})
    else:
        return jsonify({"error": "not found id"})
```
-----------------------------------------------
