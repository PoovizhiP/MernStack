var express = require("express");
var router=express.Router()
const { check, validationResult } = require('express-validator');  
// // i put check instead of body that is given in documentation to avoid errors
const { signout,signup,signin,webadmin, isSignedIn }= require("../controllers/auth");

// get  function only works in browser 
//balance functions are works in postman or anyother software.

router.post("/signup",
[
  check('name',"name should be at least 5 letters").isLength({min:3}),
  check('email',"it should be a email").isEmail(),
  check('password',"password should be at least 5 letters").isLength({min:3}),

],
signup);

router.post("/signin",[
  check('email',"it should be a email").isEmail(),
  check('password',"password should be at least 5 letters").isLength({min:3}),

],
signin);

router.get("/signout",signout)

router.get("/testroute",(req,res)=>{
  res.json(req.auth)
})

// router.get("/webadmin",webadmin)

module.exports=router;