const express = require("express");
const router=express.Router();

const{getOrderById,createOrder,getAllOrders,updateStatus,getOrderStatus}=require("../controllers/order")
const{isSignedIn,isAuthenticated,isAdmin}=require("../controllers/auth")
const{getUserById,pushOrderpurchaseList}=require("../controllers/user")
const {updateStock} = require("../controllers/product")

//params
router.param("userId",getUserById);
router.param("orderId",getOrderById);
//Actual  routes
//create
router.post("/order/create/:userId",isSignedIn,isAuthenticated,pushOrderpurchaseList,updateStock,createOrder);
//read
router.get("/order/all/:userId",isSignedIn,isAdmin,isAuthenticated,getAllOrders);

//status
router.get("/order/status/:userId",isSignedIn,isAuthenticated,isAdmin,getOrderStatus)
router.put("/order/:orderId/status/:userId",isSignedIn,isAdmin,isAuthenticated,updateStatus)

module.exports=router;