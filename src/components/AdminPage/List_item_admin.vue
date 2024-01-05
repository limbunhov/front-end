<template>
    <section class="on off">
        <div class="board_admin">
            <div class="profile_admin">
                <div class="pro_img">
                    <i class="fa-solid fa-user"></i>
                </div>
                <div class="name">
                    <a href="#">Admin</a>
                </div>
            </div>
            <div class="filter_pro">
                <input type="text" placeholder="Search...">
                <span><i class="fa-solid fa-magnifying-glass"></i></span>
            </div>
            <div class="sort_by">
                <div class="text_sort">
                    <span>Short by:</span>
                </div>
                <div class="dropdown">
                    <a class="btn btn-secondary dropdown-toggle" href="#" role="button" data-bs-toggle="dropdown"
                        aria-expanded="false">
                        Default
                    </a>
                    <ul class="dropdown-menu">
                        <li><a class="dropdown-item" href="#">Action</a></li>
                        <li><a class="dropdown-item" href="#">Another action</a></li>
                        <li><a class="dropdown-item" href="#">Something else here</a></li>
                    </ul>
                </div>
            </div>
            <div class="card_product">
                <div class="card_admin">
                    <div class="p1">
                        <img src="../../assets/macbook_air.jpg" alt="">
                        <div class="icons">
                            <i class="fa-solid fa-trash"></i>
                            <i class="fa-solid fa-pen-to-square"></i>
                        </div>
                    </div>
                    <div class="details">
                        <h1>Macbook Air 13.6 <sup>"</sup> </h1>
                        <div class="warranty">
                            <span>Available in Stock </span>
                            <span>1 year warranty </span>
                            <p>Macbook Pro 14” M2 Max-32GB-1TB(Space Grey)</p>
                        </div>
                        <div>
                            <p>&#10004; Apple M2 Chip</p>
                            <p>&#10004; 8-Core CPU & 8-Core GPU</p>
                            <p>&#10004; 8GB Unified Ram</p>
                            <p>&#10004; 256GB SSD PCIe</p>
                            <p>&#10004; 13.6" Liquid Retina Display</p>
                        </div>
                    </div>
                    <div class="prices">
                        <h1>$1,149</h1>
                    </div>
                </div>

            </div>
        </div>
    </section>
    <section class="on ">
        <div class="board_admin">
            <div class="profile_admin">
                <div class="pro_img">
                    <i class="fa-solid fa-user"></i>
                </div>
                <div class="name">
                    <a href="#">Admin</a>
                </div>
            </div>
            <div class="card_box">
                <div class="style_card">
                    <div class="input_infor">
                        <label>Product Name</label>
                        <input type="text">
                        <label>Price</label>
                        <input type="text">
                        <div class="d-flex gap-3 item">
                            <div class="d-flex flex-column">
                                <label>categary</label>
                                <input type="text" name="" id="">
                            </div>
                            <div class="d-flex flex-column">
                                <label for="">Year</label>
                                <input type="text">
                            </div>
                        </div>
                        <label for="">Brand</label>
                        <input type="text">
                        <label for="">Description</label>
                        <textarea class="form-control"></textarea>
                    </div>
                    <div class="add_infor">
                        <div class="all_img">
                            <div>
                                <input type="file" id="file">
                                <label for="file" class="d-flex flex-column"><span><i
                                            class="fa-solid fa-image"></i></span><span>Add image</span></label>
                            </div>
                            <div class="two_pic">
                                <div>
                                    <input type="file" id="file">
                                    <label for="file" class="d-flex flex-column">
                                        <i class="fa-solid fa-plus"></i></label>
                                </div>
                                <div>
                                    <input type="file" id="file">
                                    <label for="file" class="d-flex flex-column">
                                        <i class="fa-solid fa-plus"></i></label>
                                </div>
                            </div>
                        </div>
                        <button class="btn bg-primary text-white">Add product</button>
                    </div>
                </div>
            </div>
        </div>
    </section>
</template>