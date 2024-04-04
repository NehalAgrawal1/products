// product.entity.ts
import { Entity, PrimaryGeneratedColumn, Column } from 'typeorm';

@Entity()
export class Product {
  @PrimaryGeneratedColumn()
  id: number;

  @Column()
  name: string;

  @Column()
  description: string;

  @Column()
  price: number;

  @Column()
  category: string;

  @Column()
  image: string;
}

// product.service.ts
import { Injectable } from '@nestjs/common';
import { InjectRepository } from '@nestjs/typeorm';
import { Repository } from 'typeorm';
import { Product } from './product.entity';

@Injectable()
export class ProductService {
  constructor(
    @InjectRepository(Product)
    private readonly productRepository: Repository<Product>,
  ) {}

  async getProductCategories(): Promise<string[]> {
    // Implementation to fetch unique product categories from the database
  }

  async getProductsByCategory(category: string): Promise<Product[]> {
    // Implementation to fetch products by category from the database
  }

  async getProductById(id: number): Promise<Product> {
    // Implementation to fetch product by id from the database
  }
}

// product.controller.ts
import { Controller, Get, Param } from '@nestjs/common';
import { ProductService } from './product.service';
import { Product } from './product.entity';

@Controller('products')
export class ProductController {
  constructor(private readonly productService: ProductService) {}

  @Get('categories')
  async getProductCategories(): Promise<string[]> {
    return this.productService.getProductCategories();
  }

  @Get('category/:category')
  async getProductsByCategory(@Param('category') category: string): Promise<Product[]> {
    return this.productService.getProductsByCategory(category);
  }

  @Get(':id')
  async getProductById(@Param('id') id: number): Promise<Product> {
    return this.productService.getProductById(id);
  }
}
